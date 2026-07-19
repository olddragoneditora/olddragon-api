Autenticação
============

A API usa OAuth 2.0 com OpenID Connect para autenticação segura. PKCE é obrigatório para o fluxo de authorization code.

## Registro de Aplicação

Cadastre sua aplicação em [olddragon.com.br/conta/aplicativos](https://olddragon.com.br/conta/aplicativos) (Aplicativos para Desenvolvedores) — o cadastro é self-service, não é preciso pedir aprovação por email. Informe:

1. Nome da aplicação
2. Descrição da funcionalidade (opcional)
3. URL da página inicial (`homepage_url`) — precisa começar com `http://` ou `https://`
4. URL de callback (`redirect_uri`, ex: `https://seu-app.com/callback`) — precisa começar com `http://` ou `https://`
5. Escopos desejados (veja "Scopes Disponíveis" abaixo)

Você recebe imediatamente:
- `client_id`: Identificador público da aplicação
- `client_secret`: Chave secreta — **exibida uma única vez**, no momento em que é criada ou regenerada. Guarde-a em local seguro; se perdê-la, é preciso regenerar (o que invalida a anterior na hora).

Limite de 5 aplicativos por conta. Você pode mudar depois qualquer informação (até o nome) da sua aplicação, ou excluí-la, em "Aplicativos para Desenvolvedores".

Aplicações que não conseguem guardar um `client_secret` com segurança (desktop, CLI, um módulo de jogo) não devem usar o fluxo padrão abaixo — use o Device Flow (seção "Aplicativos de Desktop e Auto-Hospedados" mais adiante neste documento), que dispensa client secret. Não há alternância pública/confidencial no formulário de cadastro.

## Por que Autenticar?

A autenticação permite acesso a:
- **Conteúdo exclusivo**: Monstros, magias e equipamentos de livros comprados
- **Dados pessoais**: Personagens e campanhas do usuário
- **Funcionalidades avançadas**: Edição de personagens, gerenciamento de campanhas

Exemplo: O monstro "Normósia" só está disponível para quem possui o livro "ARKHI".

## Configuração OAuth 2.0

### Endpoints
- **Discovery**: `https://olddragon.com.br/.well-known/openid-configuration`
- **Authorization**: `https://olddragon.com.br/authorize`
- **Token**: `https://olddragon.com.br/token`
- **User Info**: `https://olddragon.com.br/userinfo`

### Parâmetros Obrigatórios

#### Authorization Request
```
https://olddragon.com.br/authorize?
  client_id=SEU_CLIENT_ID&
  redirect_uri=https://seu-app.com/callback&
  response_type=code&
  scope=openid email content.read offline_access&
  code_challenge=CODIGO_CHALLENGE&
  code_challenge_method=S256&
  prompt=consent
```

### Scopes Disponíveis
- `openid`: Informações básicas do usuário
- `email`: Email do usuário
- `content.read`: Ler seus personagens, campanhas e conteúdo dos seus livros — exigido em toda requisição `GET`/`HEAD`
- `content.write`: Criar e alterar seus personagens, campanhas, ajudantes e conteúdo caseiro — exigido em qualquer requisição que não seja `GET`/`HEAD` (`POST`, `PUT`, `PATCH`, `DELETE`)
- `offline_access`: Refresh token para acesso prolongado

### Validade dos Tokens
- **Authorization Code**: 5 minutos
- **Access Token**: 1 hora
- **Refresh Token**: 1 ano (com `offline_access`)

### Renovação de Token

Quando receber erro 401, use o refresh token:

#### cURL
```bash
curl -X POST https://olddragon.com.br/token \
  -d "grant_type=refresh_token" \
  -d "refresh_token=SEU_REFRESH_TOKEN" \
  -d "client_id=SEU_CLIENT_ID"
```

#### HTTPie
```bash
http --form POST https://olddragon.com.br/token \
  grant_type=refresh_token \
  refresh_token=SEU_REFRESH_TOKEN \
  client_id=SEU_CLIENT_ID
```

## Aplicativos de Desktop e Auto-Hospedados (Device Flow)

Aplicativos sem navegador embutido ou sem como guardar um `client_secret` com
segurança — um módulo de jogo, um script auto-hospedado — usam o Device
Authorization Grant (RFC 8628) em vez do fluxo padrão de authorization code acima.
Não é necessário `client_secret` em nenhuma etapa.

### 1. Solicitar um código de dispositivo

#### cURL
```bash
curl -X POST https://olddragon.com.br/device-authorization \
  -d "client_id=SEU_CLIENT_ID" \
  -d "scope=content.read content.write offline_access"
```

#### HTTPie
```bash
http --form POST https://olddragon.com.br/device-authorization \
  client_id=SEU_CLIENT_ID \
  scope="content.read content.write offline_access"
```

Resposta:
```json
{
  "device_code": "...",
  "user_code": "ABCD1234",
  "verification_uri": "https://olddragon.com.br/dispositivo",
  "verification_uri_complete": "https://olddragon.com.br/dispositivo?user_code=ABCD1234",
  "expires_in": 300,
  "interval": 5
}
```

### 2. Usuário verifica o código

Mostre o `user_code` (ou o link `verification_uri_complete`, que já preenche o
código) para o usuário. Ele acessa `verification_uri`, faz login se necessário e
confirma o código — a aplicação não precisa fazer mais nada nesta etapa além de
aguardar.

### 3. Fazer polling do token

Enquanto o usuário não confirma, faça polling em `/token` a cada `interval`
segundos (5s por padrão):

#### cURL
```bash
curl -X POST https://olddragon.com.br/token \
  -d "grant_type=urn:ietf:params:oauth:grant-type:device_code" \
  -d "device_code=SEU_DEVICE_CODE" \
  -d "client_id=SEU_CLIENT_ID"
```

#### HTTPie
```bash
http --form POST https://olddragon.com.br/token \
  grant_type=urn:ietf:params:oauth:grant-type:device_code \
  device_code=SEU_DEVICE_CODE \
  client_id=SEU_CLIENT_ID
```

Antes da confirmação, a resposta é `400` com um destes erros em `error`:

| `error` | Significado | O que fazer |
|---|---|---|
| `authorization_pending` | Usuário ainda não confirmou | Continue o polling no intervalo indicado |
| `slow_down` | Polling mais rápido que o intervalo | Aumente o intervalo e continue |
| `expired_token` | `device_code` expirou (`expires_in`, 5 minutos) | Reinicie o fluxo a partir do passo 1 |
| `access_denied` | Usuário negou ou revogou o acesso | Reinicie o fluxo a partir do passo 1 |

Após a confirmação, a mesma requisição retorna `200` com `access_token` (e
`refresh_token`, se `offline_access` foi solicitado) — igual ao fluxo padrão de
authorization code.

## Importante: Use Bibliotecas OAuth Estabelecidas

**Implementar OAuth 2.0 com PKCE manualmente é perigoso e não recomendado.** Use sempre bibliotecas OAuth estabelecidas:

### Por que usar bibliotecas?

- **Segurança**: Previne vulnerabilidades comuns (CSRF, vazamento de tokens, replay attacks)
- **PKCE correto**: Geração segura de `code_verifier` e `code_challenge`
- **Validação de estado**: Proteção contra ataques de cross-site request forgery
- **Gerenciamento de tokens**: Renovação automática e armazenamento seguro
- **Conformidade**: Implementação completa das especificações RFC

### Bibliotecas Recomendadas

| Linguagem | Biblioteca |
|-----------|------------|
| JavaScript | `passport-oauth2` |
| Python | `authlib` |
| Ruby | `omniauth-oauth2` |

### Riscos da Implementação Manual

**Nunca implemente OAuth manualmente** - pode resultar em:
- Vazamento de tokens de acesso
- Ataques de replay
- Vulnerabilidades CSRF
- Geração insegura de PKCE
- Validação inadequada de estado
