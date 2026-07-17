Perfis
========

Endpoints:

- [Obter meu perfil](#obter-meu-perfil)
- [Obter perfil público](#obter-perfil-publico)

Obter meu perfil
-----------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `GET /perfil.json` retorna a identidade pública do usuário autenticado (`display_name`, `bio` e `avatar_url` podem ser nulos), com contadores de recursos e links para suas coleções.

###### Exemplo de resposta JSON
<!-- START profiles_show.json -->
```json
{
  "handler": "jogador",
  "display_name": null,
  "bio": null,
  "avatar_url": null,
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
  "spells": {
    "count": 1,
    "url": "https://olddragon.com.br/magias/minhas.json"
  },
  "equipment": {
    "count": 1,
    "url": "https://olddragon.com.br/equipamentos/meus.json"
  },
  "monsters": {
    "count": 1,
    "url": "https://olddragon.com.br/monstros/meus.json"
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

* `GET /perfis/:handler.json` retorna a identidade pública de um usuário e suas criações compartilhadas.

###### Exemplo de resposta JSON
<!-- START public_profiles_show.json -->
```json
{
  "handler": "jogador",
  "display_name": null,
  "bio": null,
  "avatar_url": null,
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
  ],
  "spells": [
    {
      "id": "770e8400-e29b-41d4-a716-446655440000",
      "name": "Magia Personalizada Um",
      "url": "https://olddragon.com.br/magias/770e8400-e29b-41d4-a716-446655440000.json"
    }
  ],
  "equipment": [
    {
      "id": "880e8400-e29b-41d4-a716-446655440000",
      "name": "Equipamento Personalizado Um",
      "url": "https://olddragon.com.br/equipamentos/880e8400-e29b-41d4-a716-446655440000.json"
    }
  ],
  "monsters": [
    {
      "id": "880e8400-e29b-41d4-a716-446655440020",
      "name": "Monstro Personalizado Um",
      "url": "https://olddragon.com.br/monstros/880e8400-e29b-41d4-a716-446655440020.json"
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
