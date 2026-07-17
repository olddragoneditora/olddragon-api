Equipamentos
============

Endpoints:

- [Listar equipamentos](#listar-equipamentos)
- [Obter equipamento específico](#obter-equipamento-específico)
- [Listar meus equipamentos](#listar-meus-equipamentos)
- [Listar equipamentos comunitários](#listar-equipamentos-comunitarios)

Listar equipamentos
--------------

- `GET /equipamentos.json` retorna todos os equipamentos.

_Parâmetros opcionais de URL_:

* `ids[]` - Lista de IDs de equipamentos. Exemplo: `ids[]=adaga&ids[]=escudo`.

###### Exemplo de resposta JSON
<!-- START equipment_index.json -->
```json
[
  {
    "id": "adaga",
    "type": "Equipment",
    "name": "Adaga",
    "concept": "weapon",
    "updated_at": "2023-01-01T00:00:00.000",
    "access": "complete",
    "cost": 200,
    "damage": "1d4",
    "bonus_ca": null,
    "weight_in_load": 1,
    "weight_in_grams": null,
    "description": "Pequena, Perfurante, Arremesso (9)\n",
    "fontes": [
      {
        "page": 58,
        "compact": false,
        "digital_item_url": "https://olddragon.com.br/livros/lb1.json"
      }
    ],
    "url": "https://olddragon.com.br/equipamentos/adaga.json"
  },
  {
    "id": "escudo",
    "type": "Equipment",
    "name": "Escudo",
    "concept": "shield",
    "updated_at": "2023-01-01T00:00:00.000",
    "access": "complete",
    "cost": 800,
    "damage": null,
    "bonus_ca": 1,
    "weight_in_load": 1,
    "weight_in_grams": null,
    "description": "Leve, Mão Exclusiva, Madeira.\n",
    "fontes": [
      {
        "page": 60,
        "compact": false,
        "digital_item_url": "https://olddragon.com.br/livros/lb1.json"
      }
    ],
    "url": "https://olddragon.com.br/equipamentos/escudo.json"
  },
  {
    "id": "espada-curta",
    "type": "Equipment",
    "name": "Espada Curta",
    "concept": "weapon",
    "updated_at": "2023-01-01T00:00:00.000",
    "access": "complete",
    "cost": 600,
    "damage": "1d6",
    "bonus_ca": null,
    "weight_in_load": 1,
    "weight_in_grams": null,
    "description": "Pequena, Cortante.",
    "fontes": [
      {
        "page": 58,
        "compact": false,
        "digital_item_url": "https://olddragon.com.br/livros/lb1.json"
      }
    ],
    "url": "https://olddragon.com.br/equipamentos/espada-curta.json"
  },
  {
    "id": "lanca",
    "type": "Equipment",
    "name": "Lança",
    "concept": "weapon",
    "updated_at": "2023-01-01T00:00:00.000",
    "access": "complete",
    "cost": 400,
    "damage": "1d6",
    "bonus_ca": null,
    "weight_in_load": 2,
    "weight_in_grams": null,
    "description": "Média, Madeira, Perfurante, Arremesso (12), Haste, Versátil, Contrainvestida.",
    "fontes": [
      {
        "page": 58,
        "compact": false,
        "digital_item_url": "https://olddragon.com.br/livros/lb1.json"
      }
    ],
    "url": "https://olddragon.com.br/equipamentos/lanca.json"
  },
  {
    "id": "tocha",
    "type": "Equipment",
    "name": "Tocha",
    "concept": "misc",
    "updated_at": "2023-01-01T00:00:00.000",
    "access": "complete",
    "cost": 100,
    "damage": null,
    "bonus_ca": null,
    "weight_in_load": null,
    "weight_in_grams": 500,
    "description": "5 unidades.\n",
    "fontes": [
      {
        "page": 62,
        "compact": false,
        "digital_item_url": "https://olddragon.com.br/livros/lb1.json"
      }
    ],
    "url": "https://olddragon.com.br/equipamentos/tocha.json"
  }
]
```
<!-- END equipment_index.json -->
###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/equipamentos.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/equipamentos.json
```

Obter equipamento específico
------------------------

- `GET /equipamentos/adaga.json` retorna o equipamento específico para a ID informada (neste exemplo, a ID é `adaga`)

###### Exemplo de resposta JSON
<!-- START equipment_show.json -->
```json
{
  "id": "adaga",
  "type": "Equipment",
  "name": "Adaga",
  "concept": "weapon",
  "updated_at": "2023-01-01T00:00:00.000",
  "access": "complete",
  "cost": 200,
  "damage": "1d4",
  "bonus_ca": null,
  "weight_in_load": 1,
  "weight_in_grams": null,
  "description": "Pequena, Perfurante, Arremesso (9)\n",
  "fontes": [
    {
      "page": 58,
      "compact": false,
      "digital_item_url": "https://olddragon.com.br/livros/lb1.json"
    }
  ],
  "url": "https://olddragon.com.br/equipamentos/adaga.json"
}
```
<!-- END equipment_show.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/equipamentos/adaga.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/equipamentos/adaga.json
```

Listar meus equipamentos
-------------------------

* `GET /equipamentos/minhas.json` retorna todos os equipamentos personalizados do usuário autenticado.

**Requer autenticação.**

###### Exemplo de resposta JSON
<!-- START equipment_my.json -->
```json
[
  {
    "id": "880e8400-e29b-41d4-a716-446655440000",
    "type": "Equipment",
    "name": "Equipamento Personalizado Um",
    "concept": "misc",
    "updated_at": "2023-01-01T00:00:00.000",
    "access": "complete",
    "cost": null,
    "damage": null,
    "bonus_ca": null,
    "weight_in_load": null,
    "weight_in_grams": null,
    "description": "Este é um equipamento customizado criado por um jogador para testes.",
    "fontes": [],
    "author": {
      "handler": "jogador",
      "url": "https://olddragon.com.br/perfis/jogador.json"
    },
    "url": "https://olddragon.com.br/equipamentos/880e8400-e29b-41d4-a716-446655440000.json"
  }
]
```
<!-- END equipment_my.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/equipamentos/minhas.json -H "Authorization: Bearer <token>"
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/equipamentos/minhas.json Authorization:"Bearer <token>"
```

Listar equipamentos comunitários
----------------------------------

* `GET /equipamentos/comunitarias.json` retorna todos os equipamentos personalizados compartilhados pela comunidade (homebrew).

_Parâmetros opcionais de URL_:

* `name` - Filtro por nome. Exemplo: `name=Espada Longa Élfica`.
* `order` - Ordenação (`name` ou `likes`). Padrão: `likes`.

###### Exemplo de resposta JSON
<!-- START equipment_homebrew.json -->
```json
[
  {
    "id": "880e8400-e29b-41d4-a716-446655440001",
    "type": "Equipment",
    "name": "Equipamento Personalizado Dois",
    "concept": "misc",
    "updated_at": "2023-01-01T00:00:00.000",
    "access": "complete",
    "cost": null,
    "damage": null,
    "bonus_ca": null,
    "weight_in_load": null,
    "weight_in_grams": null,
    "description": "Este é outro equipamento customizado criado por um jogador para testes.",
    "fontes": [],
    "author": {
      "handler": "outro_jogador",
      "url": "https://olddragon.com.br/perfis/outro_jogador.json"
    },
    "url": "https://olddragon.com.br/equipamentos/880e8400-e29b-41d4-a716-446655440001.json"
  }
]
```
<!-- END equipment_homebrew.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/equipamentos/comunitarias.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/equipamentos/comunitarias.json
```
