# Desafio Técnico · Web Dev full stack

Ficamos contentes que você tenha chegado até aqui! O desafio abaixo é baseado no nosso cotidiano e serve de pano de fundo para a entrevista técnica.

Ele tem um **mínimo**, que vale para todos, e um bloco **esperado para Pleno**. Se você se candidatou para Jr, o bloco de Pleno conta como diferencial. Em qualquer nível, trazer mais do que o pedido faz diferença na avaliação e garante um feedback detalhado, independentemente da aprovação.

## O problema: agenda da clínica Patas

A Patas é uma clínica veterinária fictícia que hoje agenda as consultas por WhatsApp e numa planilha. Ela quer um sistema simples para a recepção.

**O que fornecemos:** um arquivo com dados de exemplo (tutores, pets, veterinários e horários de atendimento) para popular o banco.

**Mínimo (todos):**

- Cadastro de tutores e pets (um tutor pode ter vários pets).
- Agendamento de consultas, com a regra de que um veterinário não pode ter duas consultas no mesmo horário e de que não se agenda fora do horário de atendimento. Essas regras ficam no backend.
- Ciclo de status da consulta: agendada → confirmada → realizada, ou cancelada. Transições inválidas (por exemplo, de cancelada para realizada) são recusadas.
- Uma tela de agenda do dia, com filtro por veterinário.
- Front, API e banco de dados. A API responde com erros claros quando algo é inválido.

**Esperado para Pleno:**

- Login com dois papéis: recepção (agenda e cadastra) e veterinário (vê a própria agenda e marca a consulta como realizada).
- Uma página pública, sem login, em que o tutor confirma ou cancela a consulta por um link único.

**Diferenciais (qualquer nível):** deploy (AWS desejável; PaaS vale), histórico de alterações de cada consulta, lembrete por e-mail, upload de documentos do pet (vacinas, exames), paginação e busca, Docker, CI, acessibilidade e responsividade.

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

O arquivo [`seed/patas.json`](seed/patas.json) tem uma lista para cada tipo de registro. Use-o para popular o seu banco do jeito que preferir: você pode manter os ids ou gerar os seus. A clínica fica em São Paulo.

| Lista | Campos |
|---|---|
| `veterinarios` | `id`, `nome`, `especialidade`, `email` |
| `horarios_atendimento` | `veterinario_id`, `dia_semana` (`segunda` a `sábado`), `inicio` e `fim` (`HH:MM`). Um veterinário pode ter mais de um turno no mesmo dia. |
| `tutores` | `id`, `nome`, `telefone` (fictício, no padrão `(11) 90000-00xx`), `email`, `criado_em` (`AAAA-MM-DD`) |
| `pets` | `id`, `tutor_id`, `nome`, `especie`, `raca`, `sexo`, `data_nascimento` (`AAAA-MM-DD`), `peso_kg`, `castrado` |

Ainda não há consultas: elas nascem no sistema que você vai construir.
