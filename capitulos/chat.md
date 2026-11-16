Chat da Campanha
================

O chat é a conversa de uma campanha: mensagens e rolagens de dados numa mesma lista, em ordem. Um programa com o token de um participante lê a conversa inteira, como o site mostra; qualquer outra pessoa lê só as rolagens. Participantes também escrevem, editam e apagam as mensagens deles, reagem e marcam o que já leram, com as mesmas regras do site.

Endpoints:

- [Ler a conversa](#ler-a-conversa)
- [Enviar uma mensagem](#enviar-uma-mensagem)
- [Editar uma mensagem](#editar-uma-mensagem)
- [Apagar uma mensagem](#apagar-uma-mensagem)
- [Reagir](#reagir)
- [Marcar como lido](#marcar-como-lido)
- [Buscar magias, monstros e outros registros](#buscar-magias-monstros-e-outros-registros)
- [Rolar dados](#rolar-dados)

Todos usam `/campanhas/ID/...`, onde `ID` é o id da campanha. Ler com um token exige o escopo `content.read` (sem token, lê-se só as rolagens); enviar, editar, apagar, reagir, marcar e rolar exigem `content.write` (veja [Autenticação](autenticacao.md)).

**Mande `Accept: application/json` junto com o token.** Uma requisição sem token recebe `401` em JSON. Já uma requisição com um token expirado, inválido ou sem o escopo necessário, e sem esse cabeçalho, recebe um `302` para `/authorize` em vez do `401` em JSON.

Quem lê e quem escreve
----------------------

O token age como a conta que o emitiu, e as regras são as da campanha:

* **Participantes** (o dono, os mestres auxiliares e os jogadores) leem mensagens e rolagens, com reações, o marcador de leitura e os números de não lidas, e escrevem, enquanto o dono mantém o chat ligado.
* **Qualquer outra pessoa** que possa ver a campanha, com ou sem token, lê só as rolagens: nenhuma mensagem chega, nem entra num contador ou num cursor. `members` vem `null`; `reactions` e `viewer.speakers` vêm vazios; `roll_account_id`, `read_at` e `newest_message_cursor` vêm `null`; `unread` e `unread_mentions` valem `0`; `viewer.can_write` é `false` e toda escrita responde `403`. Sem token, `viewer.account_id` é `null`.
* Um token só com `content.read` não escreve: a resposta é `401`.
* Com o chat desligado pelo dono (`chat_enabled: false`), todos, participantes inclusive, leem só as rolagens, como quem não participa.
* A campanha guarda as 2.000 entradas mais recentes, mensagens e rolagens juntas; as mais antigas são apagadas todo dia.
* As mensagens enviadas com um token levam a marca *via ‹aplicativo›* na conversa e `via_app` com o nome do seu aplicativo. Um aplicativo registrado em [olddragon.com.br/conta/aplicativos](https://olddragon.com.br/conta/aplicativos) aparece assim para a mesa toda.

Ler a conversa
--------------

* `GET /campanhas/ID/chat.json` devolve a página mais recente da conversa. Não exige autenticação para quem pode ver a campanha, mas só um token de participante traz as mensagens.

_Parâmetros opcionais de URL_:

* `limite` - Entradas por página, de 1 a 100. Padrão: 100.
* `antes` - Um cursor: devolve as entradas imediatamente mais antigas que ele, para rolar o histórico para trás. Use o `older_cursor` da página que você tem.
* `depois` - Um cursor: devolve, da mais antiga para a mais nova, as entradas posteriores a ele. Use o `newer_cursor` da página que você tem. É o que um programa sem websocket usa para acompanhar a conversa.

`antes` e `depois` não vão juntos. Um cursor que o servidor não emitiu responde `400` com `{"error": "..."}`. O cursor é opaco: guarde-o como veio.

Cada entrada é uma rolagem (`"type": "roll"`) ou uma mensagem (`"type": "message"`), com o outro objeto `null`. As entradas vêm da mais antiga para a mais nova, e uma página traz só uma parte delas (veja `limite`, `antes` e `depois`). A resposta é um objeto com `entries`, `members`, `viewer`, `teaser`, os cursores, os contadores, `read_at`, `more_older`, `chat_enabled` e `at`. As horas de cada entrada (`created_at`) vêm no fuso de Brasília, com microssegundos; `at` e `read_at` vêm em UTC.

###### Exemplo de resposta JSON

Lida por um token do dono da campanha, com o chat ligado e a campanha no plano pago. A conversa tem uma fala do Mestre, uma de uma conta (com o avatar do perfil, uma menção, um cartão, uma reação e a marca de editada, enviada por um aplicativo), uma de um personagem, uma rolagem de personagem, uma fala do Mestre auxiliar, uma rolagem de conta e uma mensagem com imagem:

<!-- START campaigns_chat_show.json -->
```json
{
  "entries": [
    {
      "type": "message",
      "roll": null,
      "message": {
        "id": "a1000000-0000-4000-8000-000000000001",
        "account_id": "3d576252-2ddc-525f-9d29-5a77ba87b0ce",
        "voice": "master",
        "name": "Mestre",
        "url": null,
        "color": "carmesim",
        "portrait_url": null,
        "kind": "account",
        "body": "Vocês chegam à entrada da cripta.",
        "mentions": [],
        "cards": [],
        "media": null,
        "media_expired": false,
        "edited": false,
        "mine": true,
        "can_edit": true,
        "can_delete": true,
        "via_app": null,
        "created_at": "2023-01-01T09:00:00.000000-03:00"
      },
      "reactions": [],
      "roll_account_id": null
    },
    {
      "type": "message",
      "roll": null,
      "message": {
        "id": "a1000000-0000-4000-8000-000000000002",
        "account_id": "b6a70f99-d077-5de1-8522-725ced0fdfbb",
        "voice": "account",
        "name": "@aventureiro",
        "url": null,
        "color": "verde",
        "portrait_url": "https://public.olddragon.com.br/cdn-cgi/image/height=48,format=auto/avatares/aventureiro.webp",
        "kind": "account",
        "body": "Cheguei! @jogador, lembra de Bola de Fogo?",
        "mentions": [
          {
            "account_id": "3d576252-2ddc-525f-9d29-5a77ba87b0ce",
            "color": "carmesim",
            "start": 9,
            "length": 8
          }
        ],
        "cards": [
          {
            "kind": "spell",
            "id": "bed9f51d-7517-5cce-9a19-375a092da8d3",
            "name": "Bola de Fogo",
            "summary": "Arcana 3",
            "url": "/magias/bola-de-fogo",
            "start": 29,
            "length": 12
          }
        ],
        "media": null,
        "media_expired": false,
        "edited": true,
        "mine": false,
        "can_edit": false,
        "can_delete": true,
        "via_app": "MeuApp",
        "created_at": "2023-01-01T09:01:00.000000-03:00"
      },
      "reactions": [
        {
          "kind": "laugh",
          "count": 1,
          "accounts": [
            "3d576252-2ddc-525f-9d29-5a77ba87b0ce"
          ],
          "mine": true
        }
      ],
      "roll_account_id": null
    },
    {
      "type": "message",
      "roll": null,
      "message": {
        "id": "a1000000-0000-4000-8000-000000000003",
        "account_id": "3d576252-2ddc-525f-9d29-5a77ba87b0ce",
        "voice": "character",
        "name": "Evendur",
        "url": "/personagens/59a2adaf-96e6-4569-827b-a172982cf13c",
        "color": "carmesim",
        "portrait_url": null,
        "kind": "character",
        "body": "Eu abro a porta.",
        "mentions": [],
        "cards": [],
        "media": null,
        "media_expired": false,
        "edited": false,
        "mine": true,
        "can_edit": true,
        "can_delete": true,
        "via_app": null,
        "created_at": "2023-01-01T09:02:00.000000-03:00"
      },
      "reactions": [],
      "roll_account_id": null
    },
    {
      "type": "roll",
      "roll": {
        "id": "b1000000-0000-4000-8000-000000000001",
        "kind": "character",
        "name": "Evendur",
        "url": "/personagens/59a2adaf-96e6-4569-827b-a172982cf13c",
        "portrait_url": null,
        "color": "carmesim",
        "byline": null,
        "description": "Ataque: Espada longa",
        "notation": "1d20+3",
        "result": "[20] + 3",
        "dice": [
          [
            20,
            20
          ]
        ],
        "modifier": 3,
        "total": 23,
        "verdict": "critical_hit",
        "created_at": "2023-01-01T09:03:00.000000-03:00"
      },
      "message": null,
      "reactions": [
        {
          "kind": "thumbs_up",
          "count": 1,
          "accounts": [
            "b6a70f99-d077-5de1-8522-725ced0fdfbb"
          ],
          "mine": false
        }
      ],
      "roll_account_id": "3d576252-2ddc-525f-9d29-5a77ba87b0ce"
    },
    {
      "type": "message",
      "roll": null,
      "message": {
        "id": "a1000000-0000-4000-8000-000000000004",
        "account_id": "37f7eeff-831b-5c41-984a-254965f58c0f",
        "voice": "co_master",
        "name": "Mestre auxiliar",
        "url": null,
        "color": "azul",
        "portrait_url": null,
        "kind": "account",
        "body": "Ouvem passos lá dentro.",
        "mentions": [],
        "cards": [],
        "media": null,
        "media_expired": false,
        "edited": false,
        "mine": false,
        "can_edit": false,
        "can_delete": true,
        "via_app": null,
        "created_at": "2023-01-01T09:04:00.000000-03:00"
      },
      "reactions": [],
      "roll_account_id": null
    },
    {
      "type": "roll",
      "roll": {
        "id": "b1000000-0000-4000-8000-000000000002",
        "kind": "account",
        "name": "@aventureiro",
        "url": null,
        "portrait_url": "https://public.olddragon.com.br/cdn-cgi/image/height=48,format=auto/avatares/aventureiro.webp",
        "color": "verde",
        "byline": null,
        "description": null,
        "notation": "1d6",
        "result": "[4]",
        "dice": [
          [
            6,
            4
          ]
        ],
        "modifier": 0,
        "total": 4,
        "verdict": null,
        "created_at": "2023-01-01T09:05:00.000000-03:00"
      },
      "message": null,
      "reactions": [],
      "roll_account_id": "b6a70f99-d077-5de1-8522-725ced0fdfbb"
    },
    {
      "type": "message",
      "roll": null,
      "message": {
        "id": "a1000000-0000-4000-8000-000000000005",
        "account_id": "b6a70f99-d077-5de1-8522-725ced0fdfbb",
        "voice": "account",
        "name": "@aventureiro",
        "url": null,
        "color": "verde",
        "portrait_url": "https://public.olddragon.com.br/cdn-cgi/image/height=48,format=auto/avatares/aventureiro.webp",
        "kind": "account",
        "body": "A cripta por dentro.",
        "mentions": [],
        "cards": [],
        "media": {
          "url": "https://public.olddragon.com.br/chat/cripta.webp",
          "width": 1200,
          "height": 800,
          "animated": false
        },
        "media_expired": false,
        "edited": false,
        "mine": false,
        "can_edit": false,
        "can_delete": true,
        "via_app": null,
        "created_at": "2023-01-01T09:06:00.000000-03:00"
      },
      "reactions": [],
      "roll_account_id": null
    }
  ],
  "members": [
    {
      "account_id": "3d576252-2ddc-525f-9d29-5a77ba87b0ce",
      "name": "@jogador",
      "handle": null,
      "color": "carmesim",
      "master": true,
      "sheets": [
        "Evendur"
      ]
    },
    {
      "account_id": "37f7eeff-831b-5c41-984a-254965f58c0f",
      "name": "@mestre_auxiliar",
      "handle": null,
      "color": "azul",
      "master": true,
      "sheets": []
    },
    {
      "account_id": "b6a70f99-d077-5de1-8522-725ced0fdfbb",
      "name": "@aventureiro",
      "handle": null,
      "color": "verde",
      "master": false,
      "sheets": []
    }
  ],
  "viewer": {
    "account_id": "3d576252-2ddc-525f-9d29-5a77ba87b0ce",
    "can_write": true,
    "can_send_media": true,
    "can_moderate": true,
    "can_delete_rolls": true,
    "can_report": false,
    "speakers": [
      {
        "voice": "account",
        "id": null,
        "name": "@jogador",
        "url": null,
        "portrait_url": "https://public.olddragon.com.br/cdn-cgi/image/height=48,format=auto/avatares/mestre.webp",
        "kind": "account"
      },
      {
        "voice": "master",
        "id": null,
        "name": "Mestre",
        "url": null,
        "portrait_url": null,
        "kind": "account"
      },
      {
        "voice": "character",
        "id": "59a2adaf-96e6-4569-827b-a172982cf13c",
        "name": "Evendur",
        "url": "/personagens/59a2adaf-96e6-4569-827b-a172982cf13c",
        "portrait_url": null,
        "kind": "character"
      }
    ]
  },
  "teaser": null,
  "older_cursor": "MjAyMy0wMS0wMVQxMjowMDowMC4wMDAwMDBafGExMDAwMDAwLTAwMDAtNDAwMC04MDAwLTAwMDAwMDAwMDAwMQ",
  "newer_cursor": "MjAyMy0wMS0wMVQxMjowNjowMC4wMDAwMDBafGExMDAwMDAwLTAwMDAtNDAwMC04MDAwLTAwMDAwMDAwMDAwNQ",
  "newest_message_cursor": "MjAyMy0wMS0wMVQxMjowNjowMC4wMDAwMDBafGExMDAwMDAwLTAwMDAtNDAwMC04MDAwLTAwMDAwMDAwMDAwNQ",
  "unread": 3,
  "unread_mentions": 0,
  "read_at": "2023-01-01T12:02:00.000000Z",
  "more_older": false,
  "chat_enabled": true,
  "at": "2023-01-01T12:10:00.000000Z"
}
```
<!-- END campaigns_chat_show.json -->

###### Exemplo de resposta JSON de quem não participa

O mesmo chat, lido por um token de alguém que não é da campanha: só as rolagens, e nada do que é dos participantes (`members` é `null`, e `reactions`, `roll_account_id`, `viewer.speakers` e os contadores vêm vazios):

<!-- START campaigns_chat_visitor.json -->
```json
{
  "entries": [
    {
      "type": "roll",
      "roll": {
        "id": "b1000000-0000-4000-8000-000000000001",
        "kind": "character",
        "name": "Evendur",
        "url": "/personagens/59a2adaf-96e6-4569-827b-a172982cf13c",
        "portrait_url": null,
        "color": "carmesim",
        "byline": null,
        "description": "Ataque: Espada longa",
        "notation": "1d20+3",
        "result": "[20] + 3",
        "dice": [
          [
            20,
            20
          ]
        ],
        "modifier": 3,
        "total": 23,
        "verdict": "critical_hit",
        "created_at": "2023-01-01T09:03:00.000000-03:00"
      },
      "message": null,
      "reactions": [],
      "roll_account_id": null
    },
    {
      "type": "roll",
      "roll": {
        "id": "b1000000-0000-4000-8000-000000000002",
        "kind": "account",
        "name": "@aventureiro",
        "url": null,
        "portrait_url": "https://public.olddragon.com.br/cdn-cgi/image/height=48,format=auto/avatares/aventureiro.webp",
        "color": "verde",
        "byline": null,
        "description": null,
        "notation": "1d6",
        "result": "[4]",
        "dice": [
          [
            6,
            4
          ]
        ],
        "modifier": 0,
        "total": 4,
        "verdict": null,
        "created_at": "2023-01-01T09:05:00.000000-03:00"
      },
      "message": null,
      "reactions": [],
      "roll_account_id": null
    }
  ],
  "members": null,
  "viewer": {
    "account_id": "aa67c98c-d81f-5a9c-b0bc-26caa0051aea",
    "can_write": false,
    "can_send_media": false,
    "can_moderate": false,
    "can_delete_rolls": false,
    "can_report": false,
    "speakers": []
  },
  "teaser": null,
  "older_cursor": "MjAyMy0wMS0wMVQxMjowMzowMC4wMDAwMDBafGIxMDAwMDAwLTAwMDAtNDAwMC04MDAwLTAwMDAwMDAwMDAwMQ",
  "newer_cursor": "MjAyMy0wMS0wMVQxMjowNTowMC4wMDAwMDBafGIxMDAwMDAwLTAwMDAtNDAwMC04MDAwLTAwMDAwMDAwMDAwMg",
  "newest_message_cursor": null,
  "unread": 0,
  "unread_mentions": 0,
  "read_at": null,
  "more_older": false,
  "chat_enabled": true,
  "at": "2023-01-01T12:10:00.000000Z"
}
```
<!-- END campaigns_chat_visitor.json -->

Campos:

* `entries[].roll`: a rolagem. `id`; `kind` (`character`, `retainer`, `monster`, `masked` ou `account`, quem rolou); `name` (a ficha, o monstro ou `@identificador` da conta; `?????` numa rolagem mascarada); `url` (a página da ficha ou do monstro, `null` para uma conta e uma rolagem mascarada); `portrait_url` (a imagem da ficha ou do monstro, ou o avatar do perfil de quem rolou como conta; `null` sem imagem ou mascarada); `color` (a cor da conta na campanha, `null` se saiu dela); `byline` (`{name, url}` da conta de quem rolou, quando a ficha é de outra pessoa; senão `null`); `description` (ou `null`); `notation` e `result` (como foram enviados); `dice` (`[lados, valor]` na ordem da notação, ou `null` quando o resultado não casa com a notação); `modifier` (a soma dos números fixos, ou `null` junto com `dice`); `total`; `verdict` (`success` ou `failure`, quando a rolagem tem um intervalo de sucesso; `critical_hit` ou `critical_miss` num ataque de d20, com a descrição começando por `Ataque`, sem intervalo de sucesso, que tirou 20 ou 1 no dado; senão `null`); `created_at`.
* `entries[].message`: a mensagem. `id`; `account_id` (o autor, `null` depois que a conta foi apagada, caso em que `color` é `null` e uma mensagem de conta passa a ter o nome `Conta removida`); `voice`, `name`, `url`, `portrait_url`, `kind` e `color` dizem quem fala (abaixo); `body`; `mentions[]`; `cards[]`; `media` e `media_expired`; `edited` (o texto foi editado depois do envio); `mine`, `can_edit` e `can_delete`; `via_app`; `created_at`.
* `entries[].message.voice`: `account`, `character`, `retainer`, `master` ou `co_master`. Uma mensagem `account` tem `name` `@identificador` e `kind` `account`, e traz em `portrait_url` o avatar do perfil de quem escreveu (`null` sem avatar). Uma `character` ou `retainer` tem o nome da ficha, `url` para ela, `kind` igual à voz e a imagem da ficha em `portrait_url` (`null` sem imagem); uma ficha apagada deixa a mensagem com `kind` `account` e o nome do autor, e a mesma `voice`. Uma `master` (só o dono da campanha escreve assim) tem o nome `Mestre` (`Gamemaster` para uma conta em inglês), e uma `co_master` (só os mestres auxiliares), `Mestre auxiliar` (`Co-GM`); as duas têm `kind` `account`, `portrait_url` `null` e nenhuma `url`, e `account_id` diz quem as escreveu. A voz do Mestre fica com a mensagem mesmo que o autor deixe de ser mestre.
* `entries[].message.body`: o texto como a mesa o lê, com cada menção como o `@identificador` atual do membro e cada cartão como o nome atual do registro. `mentions[]` (`account_id`, `color` e o trecho) e `cards[]` dizem onde esses nomes estão no texto, em `start` e `length` **contados em unidades UTF-16**, como um `String` de JavaScript conta. Quem saiu da campanha, ou o registro que foi apagado, deixa só o texto simples.
* `entries[].message.cards[]`: `kind` (`spell`, `monster`, `equipment`, `class` ou `race`), `id` (o UUID do registro, não o código da página), `name`, `summary` (só para registros oficiais; um registro de homebrew traz só o nome), `url`, `start` e `length`.
* `entries[].message.media`: `{url, width, height, animated}` quando a mensagem tem uma imagem; `null` sem imagem e depois que ela expirou (`media_expired: true`; o texto continua).
* `entries[].message.mine`, `can_edit`, `can_delete`: o que o dono do token pode fazer com a mensagem agora. `can_edit` vale por 15 minutos depois do envio, e só para o autor. `can_delete` vale para o autor, o dono da campanha e os mestres auxiliares.
* `entries[].message.via_app`: o nome do aplicativo OAuth que enviou a mensagem, ou `null` se veio do site.
* Uma mensagem apagada some da lista: não há marca de mensagem removida.
* `entries[].reactions[]`: as reações com contagem, na ordem dos tipos; `accounts` traz os 20 primeiros ids, e `mine` diz se o dono do token deu aquela reação. Rolagens também recebem reações.
* `entries[].roll_account_id`: a conta que fez a rolagem. É o único jeito de saber de quem é a rolagem de um monstro ou uma rolagem mascarada. Só participantes recebem; numa mensagem é sempre `null` (use `message.account_id`).
* `members[]`: os membros da campanha: `account_id`, `name` (o nome público), `handle` (o `@identificador`, ou `null` quando é o próprio `name`), `color`, `master` (o dono ou um mestre auxiliar) e `sheets` (os nomes das fichas deles na campanha). `null` para quem não participa. As cores são `rosa`, `carmesim`, `vinho`, `vermelho`, `ambar`, `amarelo`, `dourado`, `castanho`, `lima`, `verde`, `musgo`, `ciano`, `azul`, `marinho`, `lavanda`, `roxo`, `branco`, `cinza`, `grafite` e `preto`.
* `viewer`: `account_id` (`null` sem token), `can_write` (participante com o chat ligado), `can_send_media`, `can_moderate` (o dono e os mestres auxiliares), `can_delete_rolls`, `can_report` e `speakers`: as vozes que o dono do token pode usar ao escrever, cada uma com `voice`, `id` (a ficha, `null` para a conta e o Mestre), `name`, `url`, `portrait_url` e `kind` (veja [Enviar uma mensagem](#enviar-uma-mensagem)). Um jogador tem a conta e as suas fichas; o dono, também o Mestre; um mestre auxiliar, o Mestre auxiliar.
* `teaser`: `null` quando o dono da campanha é assinante. Senão, participantes leem só as 10 entradas mais recentes, mensagens e rolagens juntas, e quem não participa as 10 rolagens mais recentes; `hidden_count` conta as que o plano esconde, `master` diz se quem lê é o dono (que pode mudar o plano) e `placeholders[]` traz só a hora (`created_at`) de até 30 delas. Nenhum cursor chega às entradas escondidas, e as contagens de não lidas respeitam o mesmo limite.
* `older_cursor`, `newer_cursor`: os cursores da primeira e da última entrada da página, `null` numa página vazia. `more_older` diz se há algo antes da primeira entrada que o leitor possa ler.
* `newest_message_cursor`: o cursor da mensagem mais recente visível, qualquer que seja a página; `null` sem mensagens ou sem acesso a elas.
* `unread`, `unread_mentions`: as entradas de outras pessoas depois de `read_at` (no máximo 100) e as que mencionam o dono do token. `read_at` é o marcador de leitura dele, ou o dia em que entrou na campanha, o que for mais recente.
* `chat_enabled`: o interruptor do dono. Desligado, a conversa vira só a lista de rolagens.
* `at`: o instante em que a leitura foi feita, em UTC e com microssegundos. Duas respostas comparam como texto.

O limite é de 60 leituras por minuto por IP; acima disso a resposta é `429`, sem corpo.

### Acompanhar sem websocket

O site usa um websocket, mas nada obriga o seu programa a usá-lo. Leia a página mais recente uma vez e guarde o `newer_cursor`. De tempos em tempos (a cada poucos segundos, respeitando o limite de leituras), repita `GET chat.json?depois=CURSOR`: a resposta traz, da mais antiga para a mais nova, as entradas depois do cursor, até `limite`. Se vier uma página cheia, guarde o novo `newer_cursor` e peça de novo em seguida, até vir uma página menor. Uma página vazia tem `newer_cursor` `null`: continue com o cursor que você tinha. Para o histórico, use `antes` com o `older_cursor`. Se algo parecer fora de lugar, leia a página mais recente de novo: ela é a resposta de referência. Edições, reações novas e exclusões feitas depois aparecem na leitura da página mais recente, e não em `depois`, que só traz entradas novas.

O plano do dono da campanha vale para a leitura por API: uma campanha no plano gratuito mostra aos participantes as 10 entradas mais recentes (mensagens e rolagens juntas) e a quem só lê, as 10 rolagens mais recentes. Nenhum cursor leva às entradas escondidas: `antes` da mais antiga que você pode ler responde `more_older: false`, e `depois` de um cursor mais antigo começa na mais antiga que você pode ler.

Enviar uma mensagem
-------------------

**Autenticação obrigatória**, como participante da campanha com o chat ligado.

* `POST /campanhas/ID/chat/mensagens.json`

_Parâmetros_ (JSON, ou `multipart/form-data` com uma imagem):

* `voice` - Quem fala: `account` (a sua conta), `character` (um personagem seu na campanha), `retainer` (um ajudante seu na campanha), `master` (o Mestre, só para o dono da campanha) ou `co_master` (Mestre auxiliar, só para os mestres auxiliares).
* `speaker_id` - O id do personagem ou do ajudante, quando `voice` é `character` ou `retainer`. Uma ficha que não é sua, ou de outra campanha, é recusada. Para as outras vozes, não envie.
* `body` - O texto, de até 1.000 caracteres depois de aparado. Pode ficar vazio se houver uma imagem.
* `id` - Opcional. Um UUID escolhido por você, que torna o envio idempotente (veja abaixo).
* `media` - Opcional, só em `multipart/form-data`. Uma imagem JPEG, PNG, WebP ou GIF de até 8 MB.
* `mutation_id` - Opcional. Um texto de até 100 caracteres, devolvido como veio, para você ligar a resposta ao pedido. O cabeçalho `X-Mutation-Id` faz o mesmo.

O texto é puro: não há HTML, e os endereços de sites viram links no site. Para mencionar um participante, escreva `@[ID_DA_CONTA]` onde o nome deve ficar, com o id de `members[].account_id`: o servidor troca o trecho pelo `@identificador` do membro. Para citar um registro oficial ou seu, escreva `/[TIPO:ID_DO_REGISTRO]`, com `TIPO` um entre `spell`, `monster`, `equipment`, `class` e `race`: o servidor troca o trecho pelo nome do registro. Um trecho que não vale (alguém que não é da campanha, um registro que você não pode citar, um id malformado) some, sem erro. O servidor só consulta os 50 primeiros ids distintos do texto (menções e cartões juntos): os trechos dos demais somem do mesmo modo. No máximo 20 menções e 5 cartões contam por mensagem; o que passa disso fica como o nome em texto simples. Três recusas inteiras, todas `422`: o texto enviado passa de 8.000 bytes (contados antes da troca, mesmo que depois de aparado fique curto), passa de 1.000 caracteres depois da troca, ou, depois de trocados os trechos, sobra no texto algo com a forma de um trecho (`@[...]` ou `/[TIPO:...]`, que o servidor nunca guarda) e a mensagem toda é recusada.

###### Exemplo de requisição

```bash
curl -X POST https://olddragon.com.br/campanhas/ID/chat/mensagens.json \
     -H "Authorization: Bearer SEU_TOKEN" \
     -H "Accept: application/json" \
     -H "Content-Type: application/json" \
     -H "User-Agent: MeuApp (email@exemplo.com)" \
     -d '{"voice": "account", "body": "Cheguei, @[5a4c7e0d-1b6e-49b8-8d52-0a3f8e6c9d21]!", "id": "3b6d8a0e-5a1c-4f7e-b9d2-0c4e6a8f1b33"}'
```

###### Exemplo de resposta JSON

`201 Created`:

<!-- START campaigns_chat_messages_create.json -->
```json
{
  "mutation_id": null,
  "entry": {
    "type": "message",
    "roll": null,
    "message": {
      "id": "3b6d8a0e-5a1c-4f7e-b9d2-0c4e6a8f1b33",
      "account_id": "b6a70f99-d077-5de1-8522-725ced0fdfbb",
      "voice": "account",
      "name": "@aventureiro",
      "url": null,
      "color": "verde",
      "portrait_url": null,
      "kind": "account",
      "body": "Cheguei, @jogador!",
      "mentions": [
        {
          "account_id": "3d576252-2ddc-525f-9d29-5a77ba87b0ce",
          "color": "carmesim",
          "start": 9,
          "length": 8
        }
      ],
      "cards": [],
      "media": null,
      "media_expired": false,
      "edited": false,
      "mine": true,
      "can_edit": true,
      "can_delete": true,
      "via_app": "MeuApp",
      "created_at": "2023-01-01T09:10:00.000000-03:00"
    },
    "reactions": [],
    "roll_account_id": null
  },
  "at": "2023-01-01T12:10:00.000000Z"
}
```
<!-- END campaigns_chat_messages_create.json -->

Respostas:

* `201` - A mensagem foi criada.
* `200` com `"replayed": true` - A mesma `id`, do mesmo autor e da mesma campanha, já tinha sido salva. A resposta é a mensagem que já existe. Mande sempre uma `id` e, se a resposta se perder, repita a requisição igual: ela não diz a mesma coisa duas vezes nem converte a imagem outra vez.
* `403` `{"mutation_id", "error"}` - Você não participa da campanha, o chat está desligado, ou você enviou uma imagem sem poder (veja abaixo).
* `422` `{"mutation_id", "error", "errors"}` - A mensagem é inválida: texto vazio sem imagem, passa de 1.000 caracteres, ficha que não é sua ou de outra campanha, voz desconhecida, a voz `master` pedida por quem não é o dono da campanha, a voz `co_master` pedida por quem não é mestre auxiliar, `id` que já é de outra pessoa ou de uma rolagem. Uma requisição fora do formato esperado responde `422` só com `{"mutation_id", "error"}`.
* `409` `{"mutation_id", "cancelled": true}` - Quem enviou apagou a mensagem enquanto ela era processada (ou apagou aquele `id` nos últimos dois minutos), e nada foi salvo.
* `429` - Limite de 30 mensagens por minuto por conta, o mesmo para enviar e editar (apagar tem um limite à parte, de 120 por minuto). Uma mensagem com imagem também gasta 10 por minuto por conta e 30 por minuto por campanha.

**Imagens.** Só participantes de campanhas em que o dono é assinante e as imagens estão ligadas podem enviar `media` (`viewer.can_send_media`); caso contrário a resposta é `403`. A imagem é convertida para WebP, com no máximo 1.600 px no lado maior, e um GIF vira uma animação de até 480 px e 10 segundos. Uma imagem recusada responde `422` com a razão em `error`: grande demais, formato que não é JPEG, PNG, WebP ou GIF, ilegível, grande demais em pixels, com quadros demais (no máximo 300) ou demorada demais para converter. Um servidor ocupado responde `503` com `Retry-After: 5`: tente de novo. A campanha guarda as 300 imagens mais recentes; as mais antigas expiram e a mensagem passa a ter `media_expired: true`.

Editar uma mensagem
-------------------

**Autenticação obrigatória**, como o autor da mensagem.

* `PATCH /campanhas/ID/chat/mensagens/ID_DA_MENSAGEM.json`

_Parâmetros_ (JSON):

* `body` - O novo texto, com as mesmas regras do envio.

Só o texto muda: a voz, a ficha, a imagem e o autor ficam como estavam. O autor edita até 15 minutos depois do envio, e a mensagem passa a ter `edited: true`. Depois do prazo, ou para a mensagem de outra pessoa (nem o mestre edita a fala de um jogador), a resposta é `403`. A resposta é `{"mutation_id", "entry", "at"}`, como a do envio.

Apagar uma mensagem
-------------------

**Autenticação obrigatória**, como o autor da mensagem, o dono da campanha ou um mestre auxiliar.

* `DELETE /campanhas/ID/chat/mensagens/ID_DA_MENSAGEM.json`

A resposta é `{"mutation_id", "removed": "ID_DA_MENSAGEM"}`. O limite é de 120 apagamentos por minuto por conta, à parte do das mensagens. Um id que não é de uma mensagem desta campanha (nunca existiu, já foi apagada, é de outra campanha) responde igual, como removida, para que repetir uma exclusão seja sempre um sucesso; só um id que não é um UUID responde `404`. Todo apagamento deixa por dois minutos uma marca, de quem apagou e do id, que cancela o envio daquele mesmo id que ainda estivesse sendo processado (é assim que o site desiste de uma imagem que subia). Por isso, um envio com esse mesmo `id` nesses dois minutos é recusado com `409` `cancelled`: não reaproveite o `id` de uma mensagem que você apagou. Apagar uma mensagem com imagem apaga a imagem. Quem não é o autor nem mestre recebe `403`.

Reagir
------

**Autenticação obrigatória**, como participante da campanha com o chat ligado.

* `PUT /campanhas/ID/chat/reacoes.json` dá uma reação.
* `DELETE /campanhas/ID/chat/reacoes.json` tira a sua reação.

_Parâmetros_ (JSON):

* `entry_type` - `message` ou `roll`.
* `entry_id` - O id da mensagem ou da rolagem.
* `kind` - Um entre `thumbs_up`, `thumbs_down`, `heart`, `laugh`, `cry`, `surprised`, `tongue`, `fear`, `wave`, `celebrate`, `cheers`, `fire`, `sword`, `skull`, `monster` e `horror`.

Cada conta dá cada reação uma vez por entrada, e repetir qualquer um dos dois pedidos não faz mal. A resposta traz as reações da entrada como estão agora:

<!-- START campaigns_chat_reactions_update.json -->
```json
{
  "mutation_id": null,
  "entry_type": "message",
  "entry_id": "b2d0b3a8-4c2f-4a9e-9d38-3d9c0e5a7a42",
  "reactions": [
    {
      "kind": "laugh",
      "count": 2,
      "accounts": [
        "b6a70f99-d077-5de1-8522-725ced0fdfbb",
        "3d576252-2ddc-525f-9d29-5a77ba87b0ce"
      ],
      "mine": true
    }
  ],
  "at": "2023-01-01T12:10:00.000000Z"
}
```
<!-- END campaigns_chat_reactions_update.json -->

Uma entrada que não existe, é de outra campanha ou está escondida pelo plano responde `404`. Limite de 60 por minuto por conta.

Marcar como lido
----------------

**Autenticação obrigatória**, como participante da campanha com o chat ligado.

* `POST /campanhas/ID/chat/lido.json`

_Parâmetros_ (JSON):

* `cursor` - Um cursor emitido pelo servidor (por exemplo, o `newer_cursor` da página que você leu). O marcador vai para a hora dele, só para a frente e nunca além do relógio do servidor.

A resposta é `{"mutation_id"}`; um cursor que não vale responde `400`. O marcador é o que faz `unread` ser o mesmo em todos os aparelhos. Limite de 60 por minuto por conta.

Buscar magias, monstros e outros registros
-------------------------------------------

**Autenticação obrigatória**, como participante da campanha com o chat ligado.

* `GET /campanhas/ID/chat/referencias.json?tipo=magia&q=bola`

_Parâmetros de URL_:

* `tipo` - Obrigatório: `magia`, `monstro`, `item`, `classe` ou `raca`. Qualquer outro valor responde `422`.
* `q` - O trecho do nome. Com menos de dois caracteres só voltam os seus próprios registros de homebrew; o texto é cortado em 100 caracteres.

A resposta traz até 8 registros que você pode citar: primeiro os oficiais de livros já lançados, depois os seus de homebrew (`own: true`), e nunca os de outras pessoas. Escreva o trecho `/[TIPO:ID]` de uma mensagem com o `type` e o `id` da resposta. O `id` é o UUID do registro: o código da página (`bola-de-fogo`, o final de `url`) não serve, e um trecho com ele é descartado do texto sem aviso.

<!-- START campaigns_chat_references_index.json -->
```json
{
  "references": [
    {
      "type": "spell",
      "id": "bed9f51d-7517-5cce-9a19-375a092da8d3",
      "name": "Bola de Fogo",
      "summary": "Arcana 3",
      "url": "/magias/bola-de-fogo",
      "own": false
    }
  ]
}
```
<!-- END campaigns_chat_references_index.json -->

Limite de 60 por minuto por conta. Um registro que você não pode citar (de outra pessoa, ou de um livro ainda não lançado) não aparece, e um trecho `/[TIPO:ID]` para ele é descartado do texto sem aviso.

Rolar dados
-----------

**Autenticação obrigatória**, como participante da campanha.

* `POST /campanhas/ID/rolagens.json` faz uma rolagem na campanha. A rolagem entra na lista do chat para todos os leitores.

_Parâmetros_ (JSON, dentro de `dice_roll`):

* `notation` - A notação (por exemplo, `1d20+3`), com até 64 caracteres.
* `result` - O resultado dos dados, como `[17] + 3`, com até 255 caracteres. Quem rola no seu programa informa o resultado.
* `description` - Opcional, até 255 caracteres.
* `character_id`, `retainer_id`, `monster_id` - Opcionais: a ficha em nome de quem a rolagem sai, e só uma delas. Sem nenhuma, a rolagem sai em nome da sua conta.
* `masked` - Opcional, para o mestre: esconde o nome de um monstro (`?????`).
* `success` - Opcional, o intervalo de sucesso, como `1-10`.

A resposta é `{"masked": false}`. Limite de 30 por minuto por conta. Uma rolagem não confere a voz como uma mensagem: use `viewer.speakers` para saber que fichas são suas. As rolagens que o chat faz no site passam por este mesmo endpoint.

Erros
-----

| Código | Quando |
|--------|--------|
| `400` | Cursor inválido em `chat.json` ou em `chat/lido`. |
| `401` | Token ausente, expirado ou sem o escopo (com `Accept: application/json`). |
| `403` | Não participa da campanha, chat desligado, edição fora do prazo ou da mensagem de outra pessoa, imagem sem plano. |
| `404` | Mensagem, rolagem ou campanha que não existe (ou entrada que o plano esconde). |
| `409` | Envio cancelado por uma exclusão que chegou antes. |
| `422` | Texto ou parâmetros inválidos, voz ou ficha que não são suas, imagem recusada. |
| `429` | Limite de requisições. Espere e tente de novo. |
| `503` | Servidor ocupado convertendo imagens. Tente de novo depois do `Retry-After`. |

As mensagens de erro vêm no idioma da conta e não devem ser comparadas como texto: decida pelo código.
