Controle de Acesso
==================

A API implementa um sistema de controle de acesso baseado nas licenças dos usuários.

## Níveis de Acesso

O campo `access` em respostas da API indica o nível de acesso:

### `limited` - Acesso Limitado
- Apenas nome e referências
- Sem estatísticas ou descrições
- **Quando**: Usuário não possui nenhuma fonte que confira acesso ao conteúdo.

### `partial` - Acesso Parcial
- Informações parciais
- Estatísticas básicas
- Descrição resumida
- **Quando**: Usuário possui ao menos uma fonte com informações parciais quanto ao conteúdo.

### `complete` - Acesso Completo
- Todas as informações disponíveis
- Estatísticas completas
- Descrições detalhadas
- Imagens e conteúdo adicional
- **Quando**: Usuário possui ao menos uma fonte completa do conteúdo.

## Exemplos de Resposta

### Com Acesso Completo
```json
{
  "id": "orc",
  "name": "Orc",
  "access": "complete",
  "pv": "6",
  "ca": "11/14",
  "attacks": [...],
  "description": "Selvagens e brutais...",
  "fontes": [
    {"page": 177, "digital_item_url": "https://olddragon.com.br/livros/lb1.json"}
  ]
}
```

### Com Acesso Limitado
```json
{
  "id": "normosia",
  "name": "Normósia",
  "access": "limited",
  "fontes": [
    {"digital_item_url": "https://olddragon.com.br/livros/arkhi.json"}
  ]
}
```

## Campo `fontes`

Toda resposta inclui `fontes` indicando:
- `digital_item_url`: URL do livro digital
- `page`: Página de referência
- `compact`: Se o livro apenas usa o conteúdo, sem apresentá-lo (libera só os números)

Use essas informações para:
1. Mostrar quais livros contêm o conteúdo
2. Criar links para aquisição
3. Indicar referências exatas

## Verificar Licenças

### Listar Livros do Usuário

#### cURL
```bash
curl -H "Authorization: Bearer TOKEN" \
     https://olddragon.com.br/livros/meus.json
```

#### HTTPie
```bash
http https://olddragon.com.br/livros/meus.json \
     Authorization:"Bearer TOKEN"
```

### Status da Assinatura

#### cURL
```bash
curl -H "Authorization: Bearer TOKEN" \
     https://olddragon.com.br/assinatura.json
```

#### HTTPie
```bash
http https://olddragon.com.br/assinatura.json \
     Authorization:"Bearer TOKEN"
```

Assinantes têm acesso completo aos livros básicos (LB1, LB2, LB3) e conteúdo exclusivo.
