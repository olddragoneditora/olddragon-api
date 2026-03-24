API Old Dragon Online
=====================

Bem-vindo à API do Old Dragon Online! Integre sua aplicação com olddragon.com.br para acessar conteúdo de RPG, personagens, campanhas e muito mais.

**Base URL**: `https://olddragon.com.br`
**Formato**: JSON apenas
**Autenticação**: OAuth 2.0 com PKCE

## Início Rápido

Confira uma demonstração de aplicação em [https://olddragon-api-nodejs-demo.fly.dev](https://olddragon-api-nodejs-demo.fly.dev) e seu código fonte em  [github.com/olddragoneditora/olddragon-api-nodejs-demo](https://github.com/olddragoneditora/olddragon-api-nodejs-demo) (você pode fazer um _fork_ e lançar uma cópia no [Fly.io](https://fly.io)).

### cURL
```bash
# Listar monstros públicos (sem autenticação)
curl -H "User-Agent: MeuApp (email@exemplo.com)" \
     https://olddragon.com.br/monstros.json

# Com autenticação OAuth
curl -H "Authorization: Bearer SEU_TOKEN" \
     -H "User-Agent: MeuApp (email@exemplo.com)" \
     https://olddragon.com.br/personagens.json
```

### HTTPie
```bash
# Listar monstros públicos (sem autenticação)
http https://olddragon.com.br/monstros.json \
     User-Agent:"MeuApp (email@exemplo.com)"

# Com autenticação OAuth
http https://olddragon.com.br/personagens.json \
     Authorization:"Bearer SEU_TOKEN" \
     User-Agent:"MeuApp (email@exemplo.com)"
```

## Suporte

Para dúvidas ou problemas, envie um email para oi@olddragon.com.br.

## Requisitos Básicos

### URLs e Protocolo
- Todas as URLs começam com `https://olddragon.com.br/`
- HTTPS obrigatório (HTTP não é suportado)
- Todas as URLs terminam com `.json`

### Cabeçalhos Obrigatórios
- `User-Agent`: Nome da aplicação e contato (ex: `MeuApp (email@exemplo.com)`)
- `Content-Type`: `application/json` (para POST/PUT)
- `Accept`: `application/json` (fortemente recomendado)

## Autenticação

A API usa OAuth 2.0 com PKCE para autenticação segura. Endpoints públicos (monstros, magias, etc.) podem ser acessados sem autenticação, mas com limitações.

### Configuração OAuth
- **Discovery URL**: `https://olddragon.com.br/.well-known/openid-configuration`
- **Authorization**: `https://olddragon.com.br/authorize`
- **Token**: `https://olddragon.com.br/token`
- **Scopes**: `openid email content.read offline_access`
- **PKCE**: Obrigatório (método S256)

### Tokens
- **Access Token**: Válido por 1 hora
- **Refresh Token**: Válido por 1 ano (requer `offline_access`)
- **Authorization Code**: Válido por 5 minutos

[Documentação completa de autenticação](capitulos/autenticacao.md)

## Paginação

Todas as coleções são paginadas automaticamente. A API retorna cabeçalhos HTTP para navegação.

### Cabeçalhos de Resposta
```http
Link: <https://olddragon.com.br/monstros.json?page=1>; rel="first",
      <https://olddragon.com.br/monstros.json?page=2>; rel="next",
      <https://olddragon.com.br/monstros.json?page=21>; rel="last"
Current-Page: 1
Total-Pages: 20
Total-Count: 400
```

### Parâmetros
- `page`: Número da página (padrão: 1)
- `per_page`: Itens por página (padrão: 20, máximo: 100)

## Cache HTTP

Use cabeçalhos HTTP para otimizar requisições:

1. Armazene `ETag` ou `Last-Modified` da primeira resposta
2. Envie como `If-None-Match` ou `If-Modified-Since` em requisições posteriores
3. Receba `304 Not Modified` se o conteúdo não mudou

## Tratamento de Erros

### Códigos de Status

| Código | Significado | Ação Recomendada |
|--------|-------------|------------------|
| 200 | Sucesso | Processar resposta |
| 304 | Não modificado | Usar cache local |
| 400 | Requisição inválida | Verificar parâmetros |
| 401 | Não autorizado | Renovar token |
| 403 | Proibido | Verificar permissões |
| 404 | Não encontrado | Não tentar novamente |
| 429 | Muitas requisições | Aguardar tempo em `Retry-After` |
| 5xx | Erro do servidor | Tentar novamente com backoff exponencial |

### Limite de Taxa
- **Padrão**: 50 requisições por 10 segundos por IP
- **Cabeçalho**: `Retry-After` indica tempo de espera em segundos

### CORS (Cross-Origin Resource Sharing)

A API suporta CORS para permitir chamadas de navegadores web:

#### Métodos Suportados
- `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `OPTIONS`

#### Headers Permitidos
- `Authorization`, `Content-Type`, `User-Agent`, e outros

## Endpoints da API

### Conteúdo Público (sem autenticação necessária)
- [Classes](capitulos/classes.md) - `/classes.json`
- [Equipamentos](capitulos/equipamentos.md) - `/equipamentos.json`
- [Livros](capitulos/livros.md) - `/livros.json`
- [Magias](capitulos/magias.md) - `/magias.json`
- [Monstros](capitulos/monstros.md) - `/monstros.json`
- [Perfis](capitulos/perfis.md) - `/perfis/:handler.json`
- [Raças](capitulos/racas.md) - `/racas.json`

**Nota**: Campanhas, personagens e ajudantes específicos (`/campanhas/ID.json`, `/personagens/ID.json` e `/ajudantes/ID.json`) podem ser acessados sem autenticação.

### Conteúdo Privado (autenticação obrigatória)
- [Ajudantes](capitulos/ajudantes.md) - `/ajudantes.json` (listar seus ajudantes)
- [Campanhas](capitulos/campanhas.md) - `/campanhas.json` (listar suas campanhas)
- [Personagens](capitulos/personagens.md) - `/personagens.json` (listar seus personagens)
- [Acesso](capitulos/acesso.md) - Controle de acesso a conteúdo exclusivo

### Níveis de Acesso ao Conteúdo
- **`limited`**: Apenas informações básicas
- **`partial`**: Informações parciais (usuário possui algumas fontes)
- **`complete`**: Acesso completo (usuário possui todas as fontes)

## Parâmetros Comuns

### Filtros de Listagem
- `ids[]`: Array de IDs específicos
- `name`: Busca por nome (quando disponível)
- `page`: Número da página
- `per_page`: Itens por página

### Exemplo com Múltiplos Filtros

#### cURL
```bash
curl "https://olddragon.com.br/monstros.json?ids[]=orc&ids[]=goblin"
```

#### HTTPie
```bash
http "https://olddragon.com.br/monstros.json?ids[]=orc&ids[]=goblin"
```

## Exemplos Práticos

### Listar Monstros com Filtros

#### cURL
```bash
curl -H "User-Agent: MeuApp (email@exemplo.com)" \
     "https://olddragon.com.br/monstros.json?concepts[]=humanoide&sizes[]=medio"
```

#### HTTPie
```bash
http "https://olddragon.com.br/monstros.json?concepts[]=humanoide&sizes[]=medio"
     User-Agent:"MeuApp (email@exemplo.com)" \
```

### Atualizar PV de Personagem

#### cURL
```bash
curl -X PUT \
     -H "Authorization: Bearer SEU_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"health_points": 15}' \
     https://olddragon.com.br/personagens/ID_PERSONAGEM/pv.json
```

#### HTTPie
```bash
http PUT https://olddragon.com.br/personagens/ID_PERSONAGEM/pv.json \
     Authorization:"Bearer SEU_TOKEN" \
     health_points=15
```

## Suporte

**Email**: oi@olddragon.com.br

## Licença

Documentação licenciada sob [Creative Commons (CC BY-SA 4.0)](http://creativecommons.org/licenses/by-sa/4.0/).
