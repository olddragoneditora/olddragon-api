Personagens
===========

Endpoints:

- [Listar personagens](#listar-personagens)
- [Obter personagem específico](#obter-personagem-específico)
- [Itens de Inventário](#itens-de-inventário)
  - [Criar item de inventário](#criar-item-de-inventário)
  - [Obter item de inventário específico](#obter-item-de-inventário-específico)
  - [Atualizar item de inventário](#atualizar-item-de-inventário)
  - [Remover item de inventário](#remover-item-de-inventário)

Campos Obsoletos
----------------

> **Aviso de Depreciação**: Os seguintes campos serão removidos no futuro próximo. Por favor, migre para os novos campos de objeto aninhado.

| Campo obsoleto | Substituição |
|----------------|--------------|
| `character_race_name`, `character_race_url` | Use o objeto `character_race` com `id`, `name`, `url` |
| `character_class_name`, `character_class_url` | Use o objeto `character_class` com `id`, `name`, `url` |
| `campaign_name`, `campaign_url` | Use o objeto `campaign` com `id`, `name`, `url` |

Listar personagens
------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `GET /personagens.json` retorna todos os personagens do usuário autenticado.

_Parâmetros opcionais de URL_:

* `ids[]` - Lista de IDs de personagens. Exemplo: `ids[]=59a2adaf-96e6-4569-827b-a172982cf13c&ids[]=59a2adaf-96e6-4569-827b-a172982cf131`.

###### Exemplo de resposta JSON
<!-- START characters_index.json -->
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
<!-- END characters_index.json -->
###### Copiar como cURL

``` shell
curl -s -H "Authorization: Bearer SEU_TOKEN" \
     https://olddragon.com.br/personagens.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/personagens.json \
     Authorization:"Bearer SEU_TOKEN"
```

Obter personagem específico
---------------------------

**Autenticação opcional**: Este endpoint pode ser acessado sem autenticação.

- `GET /personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json` retorna o personagem específica para a ID informada (neste exemplo, a ID é `59a2adaf-96e6-4569-827b-a172982cf13c`).

###### Exemplo de resposta JSON
<!-- START characters_show.json -->
```json
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
```
<!-- END characters_show.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json
```

### Seleções de Habilidades Raciais (Race Mechanic Selections)

O campo `race_mechanic_selections` contém as escolhas que o jogador fez para habilidades raciais que requerem seleção durante a criação do personagem.

**Importante**: Este array só aparece quando o personagem possui habilidades raciais que requerem uma escolha do jogador. A maioria das habilidades raciais é aplicada automaticamente e não requer seleção.

#### Quando uma seleção é necessária

Nem todas as habilidades raciais requerem seleção. Existem dois tipos de habilidades que exigem escolha do jogador:

1. **Bônus em Jogada de Proteção (`bonus_jp`)**: O jogador escolhe qual JP recebe o bônus
   - Exemplo: Humanos podem escolher entre `jpc`, `jpd` ou `jps`
   - Apenas uma escolha é permitida por habilidade

2. **Construção Variável (`variable_construction`)**: O jogador escolhe opções customizadas para raças especiais
   - Exemplo: Autokthon pode escolher entre arma embutida, armadura leve, arpéu, asas, etc.
   - Pode permitir escolhas personalizadas (custom) onde o jogador define nome e descrição

#### Campos do objeto de seleção

* `character_race_ability_id`: ID da habilidade racial para a qual a seleção foi feita
* `ability_name`: Nome da habilidade racial (ex: "Adaptabilidade", "Construção")
* `selection_key`: Chave da opção selecionada
  - Para `bonus_jp`: "jpc", "jpd" ou "jps"
  - Para `variable_construction`: chave da opção predefinida (ex: "arma_embutida", "armadura_leve") ou "custom" para opções personalizadas
* `custom_name` (opcional): Nome personalizado quando `selection_key` é "custom"
* `custom_description` (opcional): Descrição personalizada quando `selection_key` é "custom"

**Nota**: Para ver todas as opções disponíveis para uma habilidade racial, consulte o endpoint da raça (`/racas/:slug.json`) e verifique o campo `mechanic_config` das habilidades com `mechanic_type` igual a `bonus_jp` ou `variable_construction`.

Atualizar atributos de personagem
----------------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

- `PATCH /personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json` atualiza atributos do personagem específico para a ID informada (neste exemplo, a ID é `59a2adaf-96e6-4569-827b-a172982cf13c`).

**Parâmetros disponíveis**: Você pode atualizar um ou mais dos seguintes atributos em uma única requisição:

* `health_points`: Pontos de Vida (PV) atuais do personagem, entre 0 e o máximo de PV do personagem (legível em `max_hp` no personagem).
* `experience_points`: Experiência (XP) atuais do personagem, no mínimo 0.
* `money_gp`: Peças de ouro (PO) do personagem, no mínimo 0.
* `money_sp`: Peças de prata (PP) do personagem, no mínimo 0.
* `money_cp`: Peças de cobre (PC) do personagem, no mínimo 0.
* `notes`: Notas do personagem (texto livre).
* `resource_uses`: Usos de recursos do personagem. Listagem em formato de lista (array) de texto.

### Exemplos de uso

#### Atualizar Pontos de Vida

###### Exemplo de requisição JSON
```json
{
  "health_points": 15
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"health_points": 15}' \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  health_points:=15
```

#### Atualizar Experiência

###### Exemplo de requisição JSON
```json
{
  "experience_points": 20000
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"experience_points": 20000}' \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  experience_points:=20000
```

#### Atualizar Economia (Moedas)

###### Exemplo de requisição JSON
```json
{
  "money_gp": 100,
  "money_sp": 50,
  "money_cp": 25
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"money_gp": 100, "money_sp": 50, "money_cp": 25}' \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  money_gp:=100 \
  money_sp:=50 \
  money_cp:=25
```

#### Atualizar Notas

###### Exemplo de requisição JSON
```json
{
  "notes": "Encontrei uma chave misteriosa na última masmorra. Precisamos investigar a porta secreta no templo abandonado."
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"notes": "Encontrei uma chave misteriosa na última masmorra. Precisamos investigar a porta secreta no templo abandonado."}' \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  notes="Encontrei uma chave misteriosa na última masmorra. Precisamos investigar a porta secreta no templo abandonado."
```

#### Atualizar Múltiplos Atributos

Você pode atualizar vários atributos em uma única requisição:

###### Exemplo de requisição JSON
```json
{
  "health_points": 25,
  "experience_points": 15000,
  "money_gp": 200,
  "notes": "Nível 5 alcançado!"
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"health_points": 25, "experience_points": 15000, "money_gp": 200, "notes": "Nível 5 alcançado!"}' \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  health_points:=25 \
  experience_points:=15000 \
  money_gp:=200 \
  notes="Nível 5 alcançado!"
```

Itens de Inventário
===================

Os itens de inventário representam o equipamento, armas, armaduras e outros objetos que um personagem carrega. Cada item pode ter diversas propriedades que afetam o personagem, como peso, custo, bônus de combate, entre outros.

**Nota**: Para listar os itens de inventário de um personagem, use o endpoint [Obter personagem específico](#obter-personagem-específico), que retorna todos os dados do personagem incluindo o array `inventory_items` com todos os itens. Cada item no array inclui os campos `id` e `url` que podem ser usados para atualizar ou remover itens específicos.

Criar item de inventário
------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `POST /personagens/:character_id/inventario.json` cria um novo item de inventário para o personagem.

**Parâmetros obrigatórios**:

* `name`: Nome do item
* `concept`: Conceito/tipo do item
  - `weapon`: Arma (pode ser equipada)
  - `armor`: Armadura (pode ser equipada)
  - `shield`: Escudo (pode ser equipado)
  - `container`: Recipiente (não pode ser equipado)
  - `misc`: Diversos (não pode ser equipado)
  - `vehicle`: Veículo (não pode ser equipado)
  - `kit`: Kit de itens (não pode ser equipado)

**Parâmetros opcionais**:

* `quantity` (Quantidade): Quantidade do item (padrão: 1)
* `equipped` (Equipado?): Se o item está equipado (padrão: false)
  - **Importante**: Apenas itens com `concept` igual a `weapon`, `armor` ou `shield` podem ser equipados
  - Se você tentar equipar um item de outro tipo (como `misc`, `container`, `vehicle`, `kit`), receberá um erro de validação
* `cost` (Custo): Custo unitário em peças de cobre
* `weight_in_load` (Peso em carga): Peso em unidades de carga
* `weight_in_grams` (Peso em gramas): Peso em gramas
* `description` (Descrição): Descrição do item
* `magic_item` (Item mágico): Se é um item mágico (padrão: false)
* `damage_type` (Tipo de dano): Tipo de dano
  - `none` - Nenhum
  - `slashing` - Cortante
  - `piercing` - Perfurante
  - `bludgeoning` - Impactante
* `damage` (Dano): Dado de dano (ex: "1d6", "1d8")
* `bonus_ca` (Bônus na CA): Bônus de Classe de Armadura
* `bonus_ba` (Bônus na BA): Bônus de Ataque
* `bonus_damage` (Bônus no dano): Bônus de dano
* `increases_load_by` (Aumenta carga em): Quanto aumenta a carga do personagem (apenas para recipientes)
* `shoot_range` (Alcance disparo): Alcance de disparo em metros
* `throw_range` (Alcance arremesso): Alcance de arremesso em metros
* **Flags booleanas** (apenas para armas):
  - `arrow` (Flecha): Se é uma flecha
  - `bolt` (Virote): Se é um virote
  - `bolt_small` (Virote pequeno): Se é um virote pequeno
  - `counter_attack` (Contrainvestida): Permite contrainvestida
  - `mounted` (Montada): Arma montada
  - `polearm` (Haste): Arma de haste
  - `recharge` (Recarga): Requer recarga
  - `two_handed` (Duas mãos): Requer duas mãos
  - `versatile` (Versátil): Pode ser usada com uma ou duas mãos
  - `wooden` (Madeira): Feita de madeira

**Observação sobre campos específicos por tipo**:
- Campos de arma (`damage`, `damage_type`, `bonus_ba`, `bonus_damage`, `shoot_range`, `throw_range`, flags booleanas) são válidos apenas para itens com `concept: "weapon"`
- Campo `bonus_ca` é válido para armas, armaduras e escudos (`weapon`, `armor`, `shield`)
- Campo `increases_load_by` é válido apenas para recipientes (`concept: "container"`)

###### Exemplo de requisição JSON
```json
{
  "inventory_item": {
    "name": "Adaga",
    "concept": "weapon",
    "quantity": 1,
    "equipped": true,
    "cost": 200,
    "weight_in_load": 0,
    "description": "Pequena, Cortante ou Perfurante.",
    "damage_type": "slashing",
    "damage": "1d4"
  }
}
```

###### Exemplo de resposta JSON
<!-- START characters_inventory_items_create.json -->
```json
{
  "id": "00000000-0000-4000-a000-000000000001",
  "position": 9,
  "quantity": 1,
  "equipped": true,
  "equippable?": true,
  "name": "Adaga",
  "concept": "weapon",
  "cost": 200,
  "total_cost": 200,
  "weight_in_load": 0,
  "weight_in_grams": null,
  "sum_weight_in_grams": 0,
  "description": "Pequena, Cortante ou Perfurante.",
  "magic_item": false,
  "damage_type": "slashing",
  "damage": "1d4",
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
  "url": "https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/00000000-0000-4000-a000-000000000001.json"
}
```
<!-- END characters_inventory_items_create.json -->

###### Copiar como cURL

``` shell
curl -X POST -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"inventory_item": {"name": "Adaga", "concept": "weapon", "quantity": 1, "equipped": true, "cost": 200, "weight_in_load": 0, "description": "Pequena, Cortante ou Perfurante.", "damage_type": "slashing", "damage": "1d4"}}' \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario.json
```

###### Copiar como HTTPie

``` shell
http POST https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  inventory_item:='{"name": "Adaga", "concept": "weapon", "quantity": 1, "equipped": true, "cost": 200, "weight_in_load": 0, "description": "Pequena, Cortante ou Perfurante.", "damage_type": "slashing", "damage": "1d4"}'
```

Obter item de inventário específico
------------------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `GET /personagens/:character_id/inventario/:id.json` retorna um item de inventário específico do personagem.

###### Exemplo de resposta JSON
<!-- START characters_inventory_items_show.json -->
```json
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
}
```
<!-- END characters_inventory_items_show.json -->

###### Copiar como cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/02fd87a9-db9a-5a2e-8a95-b49e6be599c3.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/02fd87a9-db9a-5a2e-8a95-b49e6be599c3.json \
  Authorization:"Bearer $ACCESS_TOKEN"
```

Atualizar item de inventário
----------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `PATCH /personagens/:character_id/inventario/:id.json` atualiza um item de inventário existente.

Você pode atualizar qualquer um dos parâmetros listados na seção [Criar item de inventário](#criar-item-de-inventário).

###### Exemplo de requisição JSON
```json
{
  "inventory_item": {
    "equipped": false,
    "quantity": 2
  }
}
```

###### Exemplo de resposta JSON
<!-- START characters_inventory_items_update.json -->
```json
{
  "id": "02fd87a9-db9a-5a2e-8a95-b49e6be599c3",
  "position": 2,
  "quantity": 2,
  "equipped": false,
  "equippable?": true,
  "name": "Espada Curta",
  "concept": "weapon",
  "cost": 600,
  "total_cost": 1200,
  "weight_in_load": 1,
  "weight_in_grams": null,
  "sum_weight_in_grams": 2000,
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
}
```
<!-- END characters_inventory_items_update.json -->

###### Copiar como cURL

``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"inventory_item": {"equipped": false, "quantity": 2}}' \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/02fd87a9-db9a-5a2e-8a95-b49e6be599c3.json
```

###### Copiar como HTTPie

``` shell
http PATCH https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/02fd87a9-db9a-5a2e-8a95-b49e6be599c3.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  inventory_item:='{"equipped": false, "quantity": 2}'
```

Remover item de inventário
--------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `DELETE /personagens/:character_id/inventario/:id.json` remove um item de inventário do personagem.

O endpoint retorna status `204 No Content` em caso de sucesso.

###### Copiar como cURL

``` shell
curl -X DELETE -H "Authorization: Bearer $ACCESS_TOKEN" \
  https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/02fd87a9-db9a-5a2e-8a95-b49e6be599c3.json
```

###### Copiar como HTTPie

``` shell
http DELETE https://olddragon.com.br/personagens/59a2adaf-96e6-4569-827b-a172982cf13c/inventario/02fd87a9-db9a-5a2e-8a95-b49e6be599c3.json \
  Authorization:"Bearer $ACCESS_TOKEN"
```
