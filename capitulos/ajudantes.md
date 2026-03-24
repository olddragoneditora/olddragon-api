Ajudantes
=========

Ajudantes são personagens de nível 0 utilizados em aventuras no estilo funil (_funnel_). Eles possuem regras simplificadas em comparação com personagens completos:

- **Nível**: Sempre 0
- **BA (Bônus de Ataque)**: Sempre 0
- **JP (Jogada de Proteção)**: Sempre 4
- **PV (Pontos de Vida)**: 4 + modificador de Constituição (mínimo 1)
- **Ação Heroica**: Bônus único de +5 em qualquer rolagem
- **Sem classe**: Ajudantes não possuem classe de personagem

Endpoints:

- [Listar ajudantes](#listar-ajudantes)
- [Obter ajudante específico](#obter-ajudante-específico)
- [Atualizar atributos de ajudante](#atualizar-atributos-de-ajudante)
- [Itens de Inventário](#itens-de-inventário)
  - [Criar item de inventário](#criar-item-de-inventário)
  - [Obter item de inventário específico](#obter-item-de-inventário-específico)
  - [Atualizar item de inventário](#atualizar-item-de-inventário)
  - [Remover item de inventário](#remover-item-de-inventário)

Listar ajudantes
----------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `GET /ajudantes.json` retorna todos os ajudantes do usuário autenticado.

_Parâmetros opcionais de URL_:

* `ids[]` - Lista de IDs de ajudantes. Exemplo: `ids[]=91878aa9-5241-568d-8234-db5bac12778c&ids[]=91878aa9-5241-568d-8234-db5bac12778d`.

###### Exemplo de resposta JSON
<!-- START retainers_index.json -->
```json
[
  {
    "id": "91878aa9-5241-568d-8234-db5bac12778c",
    "name": "João Fazendeiro",
    "level": 0,
    "profession": "Fazendeiro",
    "created_at": "2023-01-01T00:00:00.000",
    "updated_at": "2023-01-01T00:00:00.000",
    "health_points": 5,
    "max_hp": 5,
    "injuries": 0,
    "forca": 10,
    "destreza": 12,
    "constituicao": 14,
    "inteligencia": 8,
    "sabedoria": 10,
    "carisma": 9,
    "mod_forca": 0,
    "mod_destreza": 0,
    "mod_constituicao": 1,
    "mod_inteligencia": -1,
    "mod_sabedoria": 0,
    "mod_carisma": 0,
    "ac": 10,
    "bac": 0,
    "bad": 0,
    "jp": 4,
    "jpd": 4,
    "jpc": 5,
    "jps": 4,
    "current_movement": 9,
    "movement_run": 18,
    "movement_climb": 7,
    "movement_swim": 4,
    "movement_fly": 0,
    "infravision": 0,
    "money_gp": 0,
    "money_sp": 0,
    "money_cp": 0,
    "heroic_action_used": false,
    "notes": "Um fazendeiro corajoso",
    "inventory_items": [
      {
        "id": "94629ee7-f208-53c8-9bc6-81b1dec699e8",
        "position": 0,
        "quantity": 1,
        "equipped": true,
        "equippable?": true,
        "name": "Foice",
        "concept": "weapon",
        "cost": 300,
        "total_cost": 300,
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
        "url": "https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/94629ee7-f208-53c8-9bc6-81b1dec699e8.json"
      }
    ],
    "character_race": {
      "id": "humano",
      "name": "Humano",
      "url": "https://olddragon.com.br/racas/humano.json"
    },
    "owner": {
      "handler": "jogador",
      "url": "https://olddragon.com.br/perfis/jogador.json"
    },
    "url": "https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json"
  }
]
```
<!-- END retainers_index.json -->
###### Copiar como cURL

``` shell
curl -s -H "Authorization: Bearer SEU_TOKEN" \
     https://olddragon.com.br/ajudantes.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/ajudantes.json \
     Authorization:"Bearer SEU_TOKEN"
```

Obter ajudante específico
--------------------------

**Autenticação opcional**: Este endpoint pode ser acessado sem autenticação.

- `GET /ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json` retorna o ajudante específico para a ID informada (neste exemplo, a ID é `91878aa9-5241-568d-8234-db5bac12778c`).

###### Exemplo de resposta JSON
<!-- START retainers_show.json -->
```json
{
  "id": "91878aa9-5241-568d-8234-db5bac12778c",
  "name": "João Fazendeiro",
  "level": 0,
  "profession": "Fazendeiro",
  "created_at": "2023-01-01T00:00:00.000",
  "updated_at": "2023-01-01T00:00:00.000",
  "health_points": 5,
  "max_hp": 5,
  "injuries": 0,
  "forca": 10,
  "destreza": 12,
  "constituicao": 14,
  "inteligencia": 8,
  "sabedoria": 10,
  "carisma": 9,
  "mod_forca": 0,
  "mod_destreza": 0,
  "mod_constituicao": 1,
  "mod_inteligencia": -1,
  "mod_sabedoria": 0,
  "mod_carisma": 0,
  "ac": 10,
  "bac": 0,
  "bad": 0,
  "jp": 4,
  "jpd": 4,
  "jpc": 5,
  "jps": 4,
  "current_movement": 9,
  "movement_run": 18,
  "movement_climb": 7,
  "movement_swim": 4,
  "movement_fly": 0,
  "infravision": 0,
  "money_gp": 0,
  "money_sp": 0,
  "money_cp": 0,
  "heroic_action_used": false,
  "notes": "Um fazendeiro corajoso",
  "inventory_items": [
    {
      "id": "94629ee7-f208-53c8-9bc6-81b1dec699e8",
      "position": 0,
      "quantity": 1,
      "equipped": true,
      "equippable?": true,
      "name": "Foice",
      "concept": "weapon",
      "cost": 300,
      "total_cost": 300,
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
      "url": "https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/94629ee7-f208-53c8-9bc6-81b1dec699e8.json"
    }
  ],
  "character_race": {
    "id": "humano",
    "name": "Humano",
    "url": "https://olddragon.com.br/racas/humano.json"
  },
  "owner": {
    "handler": "jogador",
    "url": "https://olddragon.com.br/perfis/jogador.json"
  },
  "url": "https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json"
}
```
<!-- END retainers_show.json -->

###### Copiar como cURL

``` shell
curl -s https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json
```

### Campos específicos de ajudantes

Os ajudantes possuem alguns campos exclusivos que não existem em personagens:

* `profession`: Profissão do ajudante (ex: "Fazendeiro", "Ferreiro", "Pescador")
* `heroic_action_used`: Se a ação heroica (+5 em qualquer rolagem) já foi utilizada
* `jp`: Jogada de Proteção base (sempre 4)

Os ajudantes **não possuem** os seguintes campos presentes em personagens:

* `experience_points`, `alignment`, `languages`, `appearance`, `personality`, `background`, `resource_uses`
* `character_class` (ajudantes não possuem classe)
* `spells` (ajudantes não possuem magias)

Atualizar atributos de ajudante
--------------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

- `PATCH /ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json` atualiza atributos do ajudante específico para a ID informada (neste exemplo, a ID é `91878aa9-5241-568d-8234-db5bac12778c`).

**Parâmetros disponíveis**: Você pode atualizar um ou mais dos seguintes atributos em uma única requisição:

* `health_points`: Pontos de Vida (PV) atuais do ajudante, entre 0 e o máximo de PV do ajudante (legível em `max_hp` no ajudante).
* `injuries`: Ferimentos do ajudante, no mínimo 0.
* `heroic_action_used`: Se a ação heroica já foi utilizada (true/false).
* `money_gp`: Peças de ouro (PO) do ajudante, no mínimo 0.
* `money_sp`: Peças de prata (PP) do ajudante, no mínimo 0.
* `money_cp`: Peças de cobre (PC) do ajudante, no mínimo 0.
* `notes`: Notas do ajudante (texto livre).

### Exemplos de uso

#### Atualizar Pontos de Vida

###### Exemplo de requisição JSON
```json
{
  "health_points": 3
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"health_points": 3}' \
  https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  health_points:=3
```

#### Usar Ação Heroica

###### Exemplo de requisição JSON
```json
{
  "heroic_action_used": true
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"heroic_action_used": true}' \
  https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  heroic_action_used:=true
```

#### Atualizar Economia (Moedas)

###### Exemplo de requisição JSON
```json
{
  "money_gp": 10,
  "money_sp": 5,
  "money_cp": 20
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"money_gp": 10, "money_sp": 5, "money_cp": 20}' \
  https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  money_gp:=10 \
  money_sp:=5 \
  money_cp:=20
```

#### Atualizar Múltiplos Atributos

Você pode atualizar vários atributos em uma única requisição:

###### Exemplo de requisição JSON
```json
{
  "health_points": 2,
  "heroic_action_used": true,
  "money_gp": 5,
  "notes": "Sobreviveu ao primeiro desafio!"
}
```

###### Copiar como cURL
``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"health_points": 2, "heroic_action_used": true, "money_gp": 5, "notes": "Sobreviveu ao primeiro desafio!"}' \
  https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json
```

###### Copiar como HTTPie
``` shell
http PATCH https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  health_points:=2 \
  heroic_action_used:=true \
  money_gp:=5 \
  notes="Sobreviveu ao primeiro desafio!"
```

Itens de Inventário
===================

Os itens de inventário representam o equipamento, armas, armaduras e outros objetos que um ajudante carrega. Cada item pode ter diversas propriedades que afetam o ajudante, como peso, custo, bônus de combate, entre outros.

**Nota**: Para listar os itens de inventário de um ajudante, use o endpoint [Obter ajudante específico](#obter-ajudante-específico), que retorna todos os dados do ajudante incluindo o array `inventory_items` com todos os itens. Cada item no array inclui os campos `id` e `url` que podem ser usados para atualizar ou remover itens específicos.

Criar item de inventário
------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `POST /ajudantes/:retainer_id/inventario.json` cria um novo item de inventário para o ajudante.

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
* `increases_load_by` (Aumenta carga em): Quanto aumenta a carga do ajudante (apenas para recipientes)
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
<!-- START retainers_inventory_items_create.json -->
```json
{
  "id": "00000000-0000-4000-b000-000000000001",
  "position": 1,
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
  "url": "https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/00000000-0000-4000-b000-000000000001.json"
}
```
<!-- END retainers_inventory_items_create.json -->

###### Copiar como cURL

``` shell
curl -X POST -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"inventory_item": {"name": "Adaga", "concept": "weapon", "quantity": 1, "equipped": true, "cost": 200, "weight_in_load": 0, "description": "Pequena, Cortante ou Perfurante.", "damage_type": "slashing", "damage": "1d4"}}' \
  https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario.json
```

###### Copiar como HTTPie

``` shell
http POST https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  inventory_item:='{"name": "Adaga", "concept": "weapon", "quantity": 1, "equipped": true, "cost": 200, "weight_in_load": 0, "description": "Pequena, Cortante ou Perfurante.", "damage_type": "slashing", "damage": "1d4"}'
```

Obter item de inventário específico
------------------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `GET /ajudantes/:retainer_id/inventario/:id.json` retorna um item de inventário específico do ajudante.

###### Exemplo de resposta JSON
<!-- START retainers_inventory_items_show.json -->
```json
{
  "id": "94629ee7-f208-53c8-9bc6-81b1dec699e8",
  "position": 0,
  "quantity": 1,
  "equipped": true,
  "equippable?": true,
  "name": "Foice",
  "concept": "weapon",
  "cost": 300,
  "total_cost": 300,
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
  "url": "https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/94629ee7-f208-53c8-9bc6-81b1dec699e8.json"
}
```
<!-- END retainers_inventory_items_show.json -->

###### Copiar como cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" \
  https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/ITEM_ID.json
```

###### Copiar como HTTPie

``` shell
http https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/ITEM_ID.json \
  Authorization:"Bearer $ACCESS_TOKEN"
```

Atualizar item de inventário
----------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `PATCH /ajudantes/:retainer_id/inventario/:id.json` atualiza um item de inventário existente.

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
<!-- START retainers_inventory_items_update.json -->
```json
{
  "id": "94629ee7-f208-53c8-9bc6-81b1dec699e8",
  "position": 0,
  "quantity": 2,
  "equipped": false,
  "equippable?": true,
  "name": "Foice",
  "concept": "weapon",
  "cost": 300,
  "total_cost": 600,
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
  "url": "https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/94629ee7-f208-53c8-9bc6-81b1dec699e8.json"
}
```
<!-- END retainers_inventory_items_update.json -->

###### Copiar como cURL

``` shell
curl -X PATCH -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"inventory_item": {"equipped": false, "quantity": 2}}' \
  https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/ITEM_ID.json
```

###### Copiar como HTTPie

``` shell
http PATCH https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/ITEM_ID.json \
  Authorization:"Bearer $ACCESS_TOKEN" \
  inventory_item:='{"equipped": false, "quantity": 2}'
```

Remover item de inventário
--------------------------

**Autenticação obrigatória**: Este endpoint requer autenticação OAuth.

* `DELETE /ajudantes/:retainer_id/inventario/:id.json` remove um item de inventário do ajudante.

O endpoint retorna status `204 No Content` em caso de sucesso.

###### Copiar como cURL

``` shell
curl -X DELETE -H "Authorization: Bearer $ACCESS_TOKEN" \
  https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/ITEM_ID.json
```

###### Copiar como HTTPie

``` shell
http DELETE https://olddragon.com.br/ajudantes/91878aa9-5241-568d-8234-db5bac12778c/inventario/ITEM_ID.json \
  Authorization:"Bearer $ACCESS_TOKEN"
```
