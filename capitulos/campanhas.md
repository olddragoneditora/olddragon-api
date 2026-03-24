Campanhas
=========

Endpoints:

- [Listar campanhas](#listar-campanhas)
- [Obter campanha específica](#obter-campanha-específica)
- [Listar personagens em uma campanha](#listar-personagens-em-uma-campanha)

Campos Obsoletos
----------------

> **Aviso de Depreciação**: Os seguintes campos serão removidos no futuro próximo. Por favor, migre para os novos campos de objeto aninhado.

| Campo obsoleto | Substituição |
|----------------|--------------|
| `personagens[].race` | Use o objeto `character_race` com `id`, `name`, `url` |
| `personagens[].class` | Use o objeto `character_class` com `id`, `name`, `url` |

Listar campanhas
----------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `GET /campanhas.json` retorna todas as campanhas do usuário autenticado.

_Parâmetros opcionais de URL_:

* `ids[]` - Lista de IDs de campanhas. Exemplo: `ids[]=261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4&ids[]=261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b5`.

###### Exemplo de resposta JSON
<!-- START campaigns_index.json -->
```json
[
  {
    "id": "261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4",
    "type": "Campaign",
    "title": "Bandeirantes de Valansia",
    "intro": "Em um mundo inexplorado, apenas os bravos se aventuram. Descubra os segredos de Valansia e torne-se um herói!\n",
    "created_at": "2023-01-01T00:00:00.000",
    "updated_at": "2023-01-01T00:00:00.000",
    "owner": {
      "handler": "jogador",
      "url": "https://olddragon.com.br/perfis/jogador.json"
    },
    "personagens": [
      {
        "id": "59a2adaf-96e6-4569-827b-a172982cf13c",
        "name": "Evendur",
        "level": 5,
        "health_points": 30,
        "max_hp": 30,
        "forca": 15,
        "destreza": 14,
        "constituicao": 12,
        "inteligencia": 10,
        "sabedoria": 9,
        "carisma": 9,
        "ac": 15,
        "created_at": "2023-01-01T00:00:00.000",
        "updated_at": "2023-01-01T00:00:00.000",
        "character_race": {
          "id": "humano",
          "name": "Humano",
          "url": "https://olddragon.com.br/racas/humano.json"
        },
        "character_class": {
          "id": "guerreiro",
          "name": "Guerreiro",
          "url": "https://olddragon.com.br/classes/guerreiro.json"
        },
        "race": "humano",
        "class": "guerreiro",
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json"
      }
    ],
    "url": "https://olddragon.com.br/campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4.json"
  }
]
```
<!-- END campaigns_index.json -->
###### Copiar como cURL

``` shell
curl -s -H "Authorization: Bearer SEU_TOKEN" \
     https://olddragon.com.br/campanhas.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/campanhas.json \
     Authorization:"Bearer SEU_TOKEN"
```

Obter campanha específica
------------------------

**Autenticação opcional**: Este endpoint pode ser acessado sem autenticação.

- `GET /campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4.json` retorna a campanha específica para a ID informada (neste exemplo, a ID é `261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4`).

###### Exemplo de resposta JSON
<!-- START campaigns_show.json -->
```json
{
  "id": "261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4",
  "type": "Campaign",
  "title": "Bandeirantes de Valansia",
  "intro": "Em um mundo inexplorado, apenas os bravos se aventuram. Descubra os segredos de Valansia e torne-se um herói!\n",
  "created_at": "2023-01-01T00:00:00.000",
  "updated_at": "2023-01-01T00:00:00.000",
  "owner": {
    "handler": "jogador",
    "url": "https://olddragon.com.br/perfis/jogador.json"
  },
  "personagens": [
    {
      "id": "59a2adaf-96e6-4569-827b-a172982cf13c",
      "name": "Evendur",
      "level": 5,
      "health_points": 30,
      "max_hp": 30,
      "forca": 15,
      "destreza": 14,
      "constituicao": 12,
      "inteligencia": 10,
      "sabedoria": 9,
      "carisma": 9,
      "ac": 15,
      "created_at": "2023-01-01T00:00:00.000",
      "updated_at": "2023-01-01T00:00:00.000",
      "character_race": {
        "id": "humano",
        "name": "Humano",
        "url": "https://olddragon.com.br/racas/humano.json"
      },
      "character_class": {
        "id": "guerreiro",
        "name": "Guerreiro",
        "url": "https://olddragon.com.br/classes/guerreiro.json"
      },
      "race": "humano",
      "class": "guerreiro",
      "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json"
    }
  ],
  "url": "https://olddragon.com.br/campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4.json"
}
```
<!-- END campaigns_show.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4.json
```

Listar personagens em uma campanha
----------------------------------

**Autenticação opcional**: Este endpoint pode ser acessado sem autenticação.

- `GET /campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4/personagens.json` retorna todos os personagens em uma campanha específica para a ID informada (neste exemplo, a ID é `261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4`).

###### Exemplo de resposta JSON
<!-- START campaigns_characters_index.json -->
```json
[
  {
    "id": "59a2adaf-96e6-4569-827b-a172982cf13c",
    "name": "Evendur",
    "level": 5,
    "created_at": "2023-01-01T00:00:00.000",
    "updated_at": "2023-01-01T00:00:00.000",
    "health_points": 30,
    "max_hp": 30,
    "injuries": 0,
    "forca": 15,
    "destreza": 14,
    "constituicao": 12,
    "inteligencia": 10,
    "sabedoria": 9,
    "carisma": 9,
    "mod_forca": 2,
    "mod_destreza": 1,
    "mod_constituicao": 0,
    "mod_inteligencia": 0,
    "mod_sabedoria": 0,
    "mod_carisma": 0,
    "ac": 15,
    "bac": 7,
    "bad": 6,
    "jpd": 9,
    "jpc": 9,
    "jps": 8,
    "current_movement": 9,
    "movement_run": 18,
    "movement_climb": 7,
    "movement_swim": 4,
    "movement_fly": 0,
    "infravision": 0,
    "experience_points": 11520,
    "money_gp": 10,
    "money_sp": 0,
    "money_cp": 0,
    "alignment": "neutro",
    "languages": [
      "Comum",
      "Anão"
    ],
    "appearance": "Bonito (Corpo); Cabelos curtos (Cabelos); Barba fechada (Geral)",
    "personality": "Humilde (Sobre todo o resto); Calmo (Sobre si mesmo); Extrovertido (Sobre outras pessoas)",
    "background": "Filho de um ferreiro das montanhas do norte de Valansia, Evendur aprendeu desde cedo o valor da honra e força em batalha.Depois de perder seu grupo de amigos, vagou até conhecer Dorgauth, o anão guerreiro, que se tornou seu irmão-em-armas e o incentivou a viver e ganhar glórias para honrar seus amigos mortos.",
    "notes": "",
    "resource_uses": [],
    "inventory_items": [
      {
        "id": "2a224ee0-ba3c-55f1-bd25-442fe7e4cde8",
        "position": 0,
        "quantity": 2,
        "equipped": false,
        "equippable?": false,
        "name": "Tocha",
        "concept": "misc",
        "cost": 100,
        "total_cost": 200,
        "weight_in_load": null,
        "weight_in_grams": 500,
        "sum_weight_in_grams": 1000,
        "description": "5 unidades.",
        "magic_item": false,
        "damage_type": "none",
        "damage": null,
        "bonus_ca": null,
        "bonus_damage": null,
        "increases_load_by": null,
        "shoot_range": null,
        "throw_range": null,
        "arrow": false,
        "bolt": false,
        "bolt_small": false,
        "counter_attack": false,
        "mounted": false,
        "polearm": false,
        "recharge": false,
        "two_handed": false,
        "versatile": false,
        "wooden": false,
        "bonus_ba": null,
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/2a224ee0-ba3c-55f1-bd25-442fe7e4cde8.json"
      },
      {
        "id": "c51b8c3b-e4a5-5fd9-8b9a-d450466ff052",
        "position": 1,
        "quantity": 1,
        "equipped": true,
        "equippable?": true,
        "name": "Espada Longa",
        "concept": "weapon",
        "cost": 1000,
        "total_cost": 1000,
        "weight_in_load": 2,
        "weight_in_grams": null,
        "sum_weight_in_grams": 2000,
        "description": "Média, Cortante.",
        "magic_item": false,
        "damage_type": "slashing",
        "damage": "1d8",
        "bonus_ca": null,
        "bonus_damage": null,
        "increases_load_by": null,
        "shoot_range": null,
        "throw_range": null,
        "arrow": false,
        "bolt": false,
        "bolt_small": false,
        "counter_attack": false,
        "mounted": false,
        "polearm": false,
        "recharge": false,
        "two_handed": false,
        "versatile": false,
        "wooden": false,
        "bonus_ba": null,
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/c51b8c3b-e4a5-5fd9-8b9a-d450466ff052.json"
      },
      {
        "id": "02fd87a9-db9a-5a2e-8a95-b49e6be599c3",
        "position": 2,
        "quantity": 1,
        "equipped": true,
        "equippable?": true,
        "name": "Espada Curta",
        "concept": "weapon",
        "cost": 600,
        "total_cost": 600,
        "weight_in_load": 1,
        "weight_in_grams": null,
        "sum_weight_in_grams": 1000,
        "description": "Pequena, Cortante.",
        "magic_item": false,
        "damage_type": "slashing",
        "damage": "1d6",
        "bonus_ca": null,
        "bonus_damage": null,
        "increases_load_by": null,
        "shoot_range": null,
        "throw_range": null,
        "arrow": false,
        "bolt": false,
        "bolt_small": false,
        "counter_attack": false,
        "mounted": false,
        "polearm": false,
        "recharge": false,
        "two_handed": false,
        "versatile": false,
        "wooden": false,
        "bonus_ba": null,
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/02fd87a9-db9a-5a2e-8a95-b49e6be599c3.json"
      },
      {
        "id": "80909d52-9daa-5d1c-8234-39574f1c9e5f",
        "position": 3,
        "quantity": 1,
        "equipped": true,
        "equippable?": true,
        "name": "Cota de Malha",
        "concept": "armor",
        "cost": 6000,
        "total_cost": 6000,
        "weight_in_load": 2,
        "weight_in_grams": null,
        "sum_weight_in_grams": 2000,
        "description": "Média, Metal.",
        "magic_item": false,
        "damage_type": "none",
        "damage": null,
        "bonus_ca": 4,
        "bonus_damage": null,
        "increases_load_by": null,
        "shoot_range": null,
        "throw_range": null,
        "arrow": false,
        "bolt": false,
        "bolt_small": false,
        "counter_attack": false,
        "mounted": false,
        "polearm": false,
        "recharge": false,
        "two_handed": false,
        "versatile": false,
        "wooden": false,
        "bonus_ba": null,
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/80909d52-9daa-5d1c-8234-39574f1c9e5f.json"
      },
      {
        "id": "8b0d8525-bb4a-5792-abaa-3876c093ed94",
        "position": 4,
        "quantity": 1,
        "equipped": false,
        "equippable?": false,
        "name": "Mochila",
        "concept": "container",
        "cost": 200,
        "total_cost": 200,
        "weight_in_load": null,
        "weight_in_grams": null,
        "sum_weight_in_grams": 0,
        "description": "De couro, com compartimentos para exploradores e reforço para peso. Adiciona 5 ao valor de carga do personagem. Comporta até 400 moedas.",
        "magic_item": false,
        "damage_type": "none",
        "damage": null,
        "bonus_ca": null,
        "bonus_damage": null,
        "increases_load_by": 5,
        "shoot_range": null,
        "throw_range": null,
        "arrow": false,
        "bolt": false,
        "bolt_small": false,
        "counter_attack": false,
        "mounted": false,
        "polearm": false,
        "recharge": false,
        "two_handed": false,
        "versatile": false,
        "wooden": false,
        "bonus_ba": null,
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/8b0d8525-bb4a-5792-abaa-3876c093ed94.json"
      },
      {
        "id": "4fcf3e9a-afa8-5f05-aae7-8dc70869be3d",
        "position": 5,
        "quantity": 1,
        "equipped": false,
        "equippable?": false,
        "name": "Corda de Cânhamo",
        "concept": "misc",
        "cost": 100,
        "total_cost": 100,
        "weight_in_load": null,
        "weight_in_grams": 2000,
        "sum_weight_in_grams": 2000,
        "description": "15 metros. Suporta erguer até 250 kg.",
        "magic_item": false,
        "damage_type": "none",
        "damage": null,
        "bonus_ca": null,
        "bonus_damage": null,
        "increases_load_by": null,
        "shoot_range": null,
        "throw_range": null,
        "arrow": false,
        "bolt": false,
        "bolt_small": false,
        "counter_attack": false,
        "mounted": false,
        "polearm": false,
        "recharge": false,
        "two_handed": false,
        "versatile": false,
        "wooden": false,
        "bonus_ba": null,
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/4fcf3e9a-afa8-5f05-aae7-8dc70869be3d.json"
      },
      {
        "id": "651ec4a3-7a51-5e36-b694-19932e6a8286",
        "position": 6,
        "quantity": 1,
        "equipped": false,
        "equippable?": false,
        "name": "Pederneira",
        "concept": "misc",
        "cost": 5,
        "total_cost": 5,
        "weight_in_load": null,
        "weight_in_grams": null,
        "sum_weight_in_grams": 0,
        "description": "Gera faíscas para acender pavios, lanternas ou fogueiras.",
        "magic_item": false,
        "damage_type": "none",
        "damage": null,
        "bonus_ca": null,
        "bonus_damage": null,
        "increases_load_by": null,
        "shoot_range": null,
        "throw_range": null,
        "arrow": false,
        "bolt": false,
        "bolt_small": false,
        "counter_attack": false,
        "mounted": false,
        "polearm": false,
        "recharge": false,
        "two_handed": false,
        "versatile": false,
        "wooden": false,
        "bonus_ba": null,
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/651ec4a3-7a51-5e36-b694-19932e6a8286.json"
      },
      {
        "id": "5ce8886b-6aca-5ea9-869f-9473099a1cef",
        "position": 8,
        "quantity": 3,
        "equipped": false,
        "equippable?": false,
        "name": "Ração de viagem",
        "concept": "misc",
        "cost": 100,
        "total_cost": 300,
        "weight_in_load": null,
        "weight_in_grams": 500,
        "sum_weight_in_grams": 1500,
        "description": "Ração diária de comida para viagem para uma pessoa.",
        "magic_item": false,
        "damage_type": "none",
        "damage": null,
        "bonus_ca": null,
        "bonus_damage": null,
        "increases_load_by": null,
        "shoot_range": null,
        "throw_range": null,
        "arrow": false,
        "bolt": false,
        "bolt_small": false,
        "counter_attack": false,
        "mounted": false,
        "polearm": false,
        "recharge": false,
        "two_handed": false,
        "versatile": false,
        "wooden": false,
        "bonus_ba": null,
        "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/5ce8886b-6aca-5ea9-869f-9473099a1cef.json"
      }
    ],
    "race_mechanic_selections": [
      {
        "character_race_ability_id": "6212eb13-e641-4049-89b4-c91c9d2b3182",
        "ability_name": "Adaptabilidade",
        "selection_key": "jpc"
      }
    ],
    "character_race": {
      "id": "humano",
      "name": "Humano",
      "url": "https://olddragon.com.br/racas/humano.json"
    },
    "character_race_name": "Humano",
    "character_race_url": "https://olddragon.com.br/racas/humano.json",
    "character_class": {
      "id": "guerreiro",
      "name": "Guerreiro",
      "url": "https://olddragon.com.br/classes/guerreiro.json"
    },
    "character_class_name": "Guerreiro",
    "character_class_url": "https://olddragon.com.br/classes/guerreiro.json",
    "campaign": {
      "id": "261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4",
      "name": "Bandeirantes de Valansia",
      "url": "https://olddragon.com.br/campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4.json"
    },
    "campaign_name": "Bandeirantes de Valansia",
    "campaign_url": "https://olddragon.com.br/campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4.json",
    "owner": {
      "handler": "jogador",
      "url": "https://olddragon.com.br/perfis/jogador.json"
    },
    "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json"
  }
]
```
<!-- END campaigns_characters_index.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4/personagens.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/campanhas/261ac8f6-6fbc-4b1e-be4a-6e5ee7d8e4b4/personagens.json
```
