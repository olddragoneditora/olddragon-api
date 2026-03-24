Autenticação
============

A API usa OAuth 2.0 com OpenID Connect para autenticação segura. PKCE é obrigatório para todas as aplicações.

## Registro de Aplicação

Para registrar sua aplicação, envie email para oi@olddragon.com.br com:

1. Nome da aplicação
2. Descrição da funcionalidade
3. URL de callback (ex: `https://seu-app.com/callback`)
4. Tipo de aplicação (web, mobile, desktop)

Você receberá:
- `client_id`: Identificador público da aplicação
- `client_secret`: Chave secreta (apenas para aplicações server-side)

Não se preocupe, você pode mudar depois qualquer informação (até o nome) da sua aplicação.

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
- `content.read`: Acesso ao conteúdo (personagens, campanhas, etc.)
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
