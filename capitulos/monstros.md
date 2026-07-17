Monstros
========

Endpoints:

- [Listar monstros](#listar-monstros)
- [Obter monstro específico](#obter-monstro-específico)
- [Listar meus monstros](#listar-meus-monstros)
- [Listar monstros comunitários](#listar-monstros-comunitarios)

Listar monstros
--------------

* `GET /monstros.json` retorna todos os monstros.

_Parâmetros opcionais de URL_:

* `ids[]` - Lista de IDs de monstros. Exemplo: `ids[]=abelhas-assassinas&ids[]=orc`.

###### Exemplo de resposta JSON
<!-- START monsters_index.json -->
```json
[
  {
    "id": "abelhas-assassinas",
    "type": "Monster",
    "name": "Abelhas assassinas",
    "flavor": "Agressivas e venenosas, fazem colmeia nos subterrâneos e tocas.",
    "concept": "inseto",
    "size": "medio",
    "habitats": [],
    "alignment": "neutro",
    "variant": false,
    "access": "limited",
    "fontes": [
      {
        "page": 114,
        "compact": false,
        "digital_item_url": "https://olddragon.com.br/livros/lb3.json"
      }
    ],
    "url": "https://olddragon.com.br/monstros/abelhas-assassinas.json"
  },
  {
    "id": "orc",
    "type": "Monster",
    "name": "Orc",
    "flavor": "Selvagens e brutais, visam a expansão de seus territórios por meio de invasões e constantes ataques aos outros povos.",
    "concept": "humanoide",
    "size": "medio",
    "habitats": [
      "qualquer"
    ],
    "alignment": "caotico",
    "variant": false,
    "access": "partial",
    "description": "  * **Classe de armadura**: possuem CA 11 ou 14 quando usam armadura de couro e escudo.\n\n  * **Infravisão**: 18 metros.",
    "encounters": "2d4",
    "encounters_lair": "1d6x10",
    "xp": "15",
    "treasure": "s",
    "treasure_lair": "b+c",
    "mv": 9,
    "mvc": null,
    "mve": null,
    "mvn": null,
    "mvv": null,
    "mvo": null,
    "dv_bonus": "1",
    "pv": "6",
    "ca": "11/14",
    "jp": "5",
    "mo": 9,
    "dv": "1",
    "attacks": [
      {
        "text": "1 × arma +3 (Arma)",
        "times": 1,
        "description": "arma",
        "ba": 3,
        "damage_description": "Arma",
        "damage": "",
        "damage_bonus": null,
        "weapon": true
      }
    ],
    "fontes": [
      {
        "page": 177,
        "compact": true,
        "digital_item_url": "https://olddragon.com.br/livros/lb1.json"
      },
      {
        "page": 141,
        "compact": false,
        "digital_item_url": "https://olddragon.com.br/livros/lb3.json"
      },
      {
        "page": null,
        "compact": true,
        "digital_item_url": "https://olddragon.com.br/livros/srd.json"
      }
    ],
    "url": "https://olddragon.com.br/monstros/orc.json"
  }
]
```
<!-- END monsters_index.json -->
###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/monstros.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/monstros.json
```

Obter monstro específico
------------------------

- `GET /monstros/orc.json` retorna o monstro específico para a ID informada (neste exemplo, a ID é `orc`).

###### Exemplo de resposta JSON
<!-- START monsters_show.json -->
```json
{
  "id": "orc",
  "type": "Monster",
  "name": "Orc",
  "flavor": "Selvagens e brutais, visam a expansão de seus territórios por meio de invasões e constantes ataques aos outros povos.",
  "concept": "humanoide",
  "size": "medio",
  "habitats": [
    "qualquer"
  ],
  "alignment": "caotico",
  "variant": false,
  "access": "partial",
  "description": "  * **Classe de armadura**: possuem CA 11 ou 14 quando usam armadura de couro e escudo.\n\n  * **Infravisão**: 18 metros.",
  "encounters": "2d4",
  "encounters_lair": "1d6x10",
  "xp": "15",
  "treasure": "s",
  "treasure_lair": "b+c",
  "mv": 9,
  "mvc": null,
  "mve": null,
  "mvn": null,
  "mvv": null,
  "mvo": null,
  "dv_bonus": "1",
  "pv": "6",
  "ca": "11/14",
  "jp": "5",
  "mo": 9,
  "dv": "1",
  "attacks": [
    {
      "text": "1 × arma +3 (Arma)",
      "times": 1,
      "description": "arma",
      "ba": 3,
      "damage_description": "Arma",
      "damage": "",
      "damage_bonus": null,
      "weapon": true
    }
  ],
  "fontes": [
    {
      "page": 177,
      "compact": true,
      "digital_item_url": "https://olddragon.com.br/livros/lb1.json"
    },
    {
      "page": 141,
      "compact": false,
      "digital_item_url": "https://olddragon.com.br/livros/lb3.json"
    },
    {
      "page": null,
      "compact": true,
      "digital_item_url": "https://olddragon.com.br/livros/srd.json"
    }
  ],
  "url": "https://olddragon.com.br/monstros/orc.json"
}
```
<!-- END monsters_show.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/monstros/orc.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/monstros/orc.json
```

Listar meus monstros
-------------------------

* `GET /monstros/minhas.json` retorna todos os monstros personalizados do usuário autenticado.

**Requer autenticação.**

###### Exemplo de resposta JSON
<!-- START monsters_my.json -->
```json
[
  {
    "id": "880e8400-e29b-41d4-a716-446655440020",
    "type": "Monster",
    "name": "Monstro Personalizado Um",
    "flavor": "",
    "concept": "humanoide",
    "size": "miudo",
    "habitats": [],
    "alignment": "ordeiro",
    "variant": false,
    "access": "complete",
    "description": "\n\n\n\n",
    "picture": null,
    "thumb_picture": null,
    "encounters": null,
    "encounters_lair": null,
    "xp": "",
    "treasure": null,
    "treasure_lair": null,
    "mv": null,
    "mvc": null,
    "mve": null,
    "mvn": null,
    "mvv": null,
    "mvo": null,
    "dv_bonus": "",
    "pv": "",
    "ca": "",
    "jp": "",
    "mo": null,
    "dv": "1",
    "attacks": [],
    "fontes": [],
    "author": {
      "handler": "jogador",
      "url": "https://olddragon.com.br/perfis/jogador.json"
    },
    "url": "https://olddragon.com.br/monstros/880e8400-e29b-41d4-a716-446655440020.json"
  }
]
```
<!-- END monsters_my.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/monstros/minhas.json -H "Authorization: Bearer <token>"
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/monstros/minhas.json Authorization:"Bearer <token>"
```

Listar monstros comunitários
----------------------------------

* `GET /monstros/comunitarias.json` retorna todos os monstros personalizados compartilhados pela comunidade (homebrew).

_Parâmetros opcionais de URL_:

* `name` - Filtro por nome. Exemplo: `name=Monstro Personalizado Dois`.
* `order` - Ordenação (`name` ou `likes`). Padrão: `likes`.

###### Exemplo de resposta JSON
<!-- START monsters_homebrew.json -->
```json
[
  {
    "id": "880e8400-e29b-41d4-a716-446655440021",
    "type": "Monster",
    "name": "Monstro Personalizado Dois",
    "flavor": "",
    "concept": "humanoide",
    "size": "miudo",
    "habitats": [],
    "alignment": "ordeiro",
    "variant": false,
    "access": "complete",
    "description": "\n\n\n\n",
    "picture": null,
    "thumb_picture": null,
    "encounters": null,
    "encounters_lair": null,
    "xp": "",
    "treasure": null,
    "treasure_lair": null,
    "mv": null,
    "mvc": null,
    "mve": null,
    "mvn": null,
    "mvv": null,
    "mvo": null,
    "dv_bonus": "",
    "pv": "",
    "ca": "",
    "jp": "",
    "mo": null,
    "dv": "1",
    "attacks": [],
    "fontes": [],
    "author": {
      "handler": "outro_jogador",
      "url": "https://olddragon.com.br/perfis/outro_jogador.json"
    },
    "url": "https://olddragon.com.br/monstros/880e8400-e29b-41d4-a716-446655440021.json"
  }
]
```
<!-- END monsters_homebrew.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/monstros/comunitarias.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/monstros/comunitarias.json
```
