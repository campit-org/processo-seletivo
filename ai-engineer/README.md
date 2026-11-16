# Desafio Técnico · AI Engineer

Ficamos contentes que você tenha chegado até aqui! O desafio abaixo é baseado no nosso cotidiano e serve de pano de fundo para a entrevista técnica.

Ele tem um **mínimo**, que vale para todos, e um bloco **esperado para Pleno**. Se você se candidatou para Jr, o bloco de Pleno conta como diferencial. Em qualquer nível, trazer mais do que o pedido faz diferença na avaliação e garante um feedback detalhado, independentemente da aprovação.

## O problema: assistente da Pedal Certo

A Pedal Certo é uma rede fictícia de lojas de bicicletas. O time de atendimento perde tempo respondendo perguntas que exigem olhar duas coisas ao mesmo tempo: os **dados da loja** (produtos, estoque por loja, pedidos) e os **documentos** (política de troca e garantia, manuais dos produtos, perguntas frequentes).

Exemplos de perguntas reais:

- "Comprei a Trilha 29 há 40 dias e o câmbio está falhando. Ainda está na garantia?"
- "Qual loja de São Paulo tem a Urbana 700 aro 28 em estoque?"
- "O pedido 10234 já foi enviado? Posso trocar o tamanho?"

**O que fornecemos:** um repositório com a base em PostgreSQL (um dump e um docker-compose para subir localmente, e os mesmos dados em CSV) e uma pasta com os documentos em Markdown e PDF.

**Mínimo (todos):**

- Um assistente que recebe uma pergunta em linguagem natural e responde usando a base, os documentos ou os dois, conforme o caso.
- A resposta diz de onde tirou a informação (a tabela ou o documento e o trecho).
- Quando não sabe ou a pergunta foge do assunto, ele diz isso em vez de inventar.
- O acesso à base é só de leitura.
- Pode ser uma API, um CLI ou uma interface simples.

**Esperado para Pleno:**

- Um jeito de saber se o assistente acerta: algumas perguntas com a resposta esperada e um script que mede.
- Como a solução rodaria em produção para 1.000 perguntas por dia: um diagrama curto, com o custo e o que pode dar errado.

**Diferenciais (qualquer nível):** memória da conversa, guardrails, interface de chat, deploy, testes automatizados, comparação entre modelos ou estratégias de busca.

**Pontos em aberto:** o enunciado deixa algumas regras sem resposta de propósito, como acontece com pedidos de cliente. Quando encontrar uma, decida, implemente e explique a decisão no README.

## Stack

Usamos Python no dia a dia, por isso ele é incentivado, mas qualquer stack é bem-vinda. Se o seu projeto envolver nuvem, AWS é fortemente desejável pelo mesmo motivo, mas outras clouds e PaaS (Railway, Vercel, Render etc.) também valem. Não exigimos que você gaste dinheiro: use o Free Tier, o LocalStack ou rode tudo localmente com Docker.

## Critérios de avaliação

As coisas que mais importam são você e as suas decisões. Queremos ter certeza de que você fez as escolhas, sabe explicar por que elas foram feitas e que foram feitas com qualidade. Não é vetado o uso de IA, desde que essas premissas sejam verdadeiras. Também avaliamos como você lida com críticas e questionamentos sobre o seu trabalho, porque a revisão entre pares é constante no nosso dia a dia.

## Requisitos do entregável

Um repositório público no GitHub, com um README que explique como rodar o projeto e as decisões que você tomou. O que você planejou e não teve tempo de fazer pode ficar documentado ou num Pull Request aberto no seu repositório.

**Para Pleno, o README também traz uma seção de decisões de produto:**

- o que você priorizou e o que deixou de fora, e por quê;
- quanto tempo levou cada parte, aproximadamente;
- quanto custaria rodar a solução por mês, com a conta;
- o que entregaria a seguir, em ordem de valor para o cliente.

Você tem 7 dias a partir do envio deste documento para entregar o desafio. Pode nos procurar para tirar dúvidas.

---

## Os dados desta pasta

```
ai-engineer/
├── docker-compose.yml   # sobe o PostgreSQL já com a base carregada
├── dump/pedal_certo.sql # esquema e dados
├── csv/                 # as mesmas tabelas, uma por arquivo
└── documentos/          # política de troca e garantia, FAQ e manuais
```

A base é um retrato do dia 27/11/2026. Datas e horas estão no horário de Brasília.

### Subindo a base

Precisa do Docker com o Compose.

```bash
cd ai-engineer
docker compose up -d --wait
```

Na primeira subida, o PostgreSQL carrega o dump sozinho. Para se conectar:

| Campo | Valor |
|---|---|
| Host | `localhost` |
| Porta | `5432` |
| Banco | `pedal_certo` |
| Usuário | `pedal_certo` |
| Senha | `pedal_certo` |

Se a porta 5432 já estiver em uso, escolha outra: `PEDAL_CERTO_PORTA=55432 docker compose up -d --wait`. Para voltar a base ao estado original, rode `docker compose down -v` e suba de novo.

### Tabelas

| Tabela | O que guarda |
|---|---|
| `lojas` | as lojas físicas e o centro de distribuição que atende o site |
| `modelos` | bicicletas, peças e acessórios à venda, com categoria, aro e preço |
| `produtos` | cada SKU: um modelo num tamanho e numa cor |
| `estoque` | quantidade de cada SKU em cada loja |
| `clientes` | clientes cadastrados |
| `pedidos` | pedidos do site e das lojas, com as datas de pagamento, envio e entrega |
| `itens_pedido` | os SKUs de cada pedido, com quantidade e preço |

O dump traz comentários nas tabelas e nas colunas que precisam de explicação (`\d+ pedidos` no `psql`). Os CSVs em `csv/` têm os mesmos dados, com cabeçalho e vírgula como separador; campos vazios são nulos.

### Documentos

| Arquivo | Conteúdo |
|---|---|
| `politica-de-troca-e-garantia.md` | desistência, troca, garantia, revisão gratuita e reembolso |
| `faq.md` | perguntas frequentes sobre pedidos, pagamento, bicicletas e lojas |
| `manual-trilha-29.pdf` | manual da mountain bike Trilha 29 |
| `manual-urbana-700.md` | manual da urbana Urbana 700 |
| `manual-eletrica-e-city.pdf` | manual da bicicleta elétrica E-City |
