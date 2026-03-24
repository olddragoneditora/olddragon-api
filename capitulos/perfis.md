Perfis
========

Endpoints:

- [Obter meu perfil](#obter-meu-perfil)
- [Obter perfil público](#obter-perfil-publico)

Obter meu perfil
-----------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `GET /perfil.json` retorna o perfil do usuário autenticado, com contadores de recursos e links para suas coleções.

###### Exemplo de resposta JSON
<!-- START profiles_show.json -->
```json
{
  "handler": "jogador",
  "url": "https://olddragon.com.br/perfis/jogador.json",
  "account": {
    "email": "jogador@olddragon.com.br"
  },
  "character_races": {
    "count": 1,
    "url": "https://olddragon.com.br/racas/minhas.json"
  },
  "character_classes": {
    "count": 1,
    "url": "https://olddragon.com.br/classes/minhas.json"
  },
  "campaigns": {
    "count": 1,
    "url": "https://olddragon.com.br/campanhas.json"
  },
  "characters": {
    "count": 6,
    "url": "https://olddragon.com.br/personagens.json"
  },
  "digital_items": {
    "count": 1,
    "url": "https://olddragon.com.br/livros/meus.json"
  }
}
```
<!-- END profiles_show.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/perfil.json -H "Authorization: Bearer <token>"
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/perfil.json Authorization:"Bearer <token>"
```

Obter perfil público
---------------------

* `GET /perfis/:handler.json` retorna o perfil público de um usuário e suas raças e classes compartilhadas.

###### Exemplo de resposta JSON
<!-- START public_profiles_show.json -->
```json
{
  "handler": "jogador",
  "url": "https://olddragon.com.br/perfis/jogador.json",
  "character_races": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "name": "Raça Personalizada Um",
      "url": "https://olddragon.com.br/racas/550e8400-e29b-41d4-a716-446655440000.json"
    }
  ],
  "character_classes": [
    {
      "id": "660e8400-e29b-41d4-a716-446655440000",
      "name": "Classe Personalizada Um",
      "url": "https://olddragon.com.br/classes/660e8400-e29b-41d4-a716-446655440000.json"
    }
  ]
}
```
<!-- END public_profiles_show.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/perfis/jogador.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/perfis/jogador.json
```
