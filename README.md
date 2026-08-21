# Esquadrão Dev Autônomo (fork do Esquadrão Dev)

> Nome provisório. Ajuste se quiser antes de adotar de vez.

## O que é isso, e como se relaciona com o Esquadrão Dev original

Este é um **fork** do framework "Esquadrão Dev" (`Esquadrao-Dev`, v3.40) — não uma versão nem uma modificação in-place. A diferença de fundo:

> **Depois da Fase 1 (Requisitos), nenhuma decisão pausa esperando um humano em tempo real.**

Todo ponto que no original é HITL bloqueante (aprovação de plano, direção visual, stack/organização de pastas, Checkpoint de Épico) vira, aqui, uma decisão que o próprio Orquestrador toma sozinho — mas **nunca silenciosamente**: toda decisão autônoma é registrada em `decisoes-autonomas.md` com fonte citada ou como ADR de decisão nova (ver seção abaixo).

## Quando usar este fork, quando usar o original

- **Use o original (`Esquadrao-Dev`)** quando você (ou outro humano) vai estar disponível para aprovar planos, direção visual e checkpoints em tempo real, tarefa por tarefa.
- **Use este fork** quando o objetivo é rodar o máximo possível sem parar para aprovação síncrona — ex: pipeline/CI, sessão longa sem supervisão, ou você prefere revisar tudo depois, em bloco, via `decisoes-autonomas.md`.

Isso **não** significa "sem controle humano nenhum". Significa que o controle humano acontece de forma assíncrona (lendo o log de decisões depois) em vez de síncrona (aprovando cada uma na hora). Ver "Freios que continuam bloqueantes" abaixo — mesmo este fork para de verdade em alguns casos.

## Diferença crítica em relação ao original: three achados corrigidos aqui

Esta versão nasceu de um diagnóstico de uma sessão real que rodou o modo autônomo e cometeu três falhas de ordem, todas com a mesma causa raiz — **tratar a narração de uma intenção como se fosse a execução real** — corrigidas nos arquivos deste fork (ver `orquestrador.md` e `agentes/01-analista-requisitos.md`):

1. **Fases declaradas "concluídas" sem o artefato existir fisicamente no disco.** A sessão escreveu "vou criar a Especificação Técnica" e seguiu como se ela já existisse, sem nunca confirmar a escrita real do arquivo.
2. **Estrutura de código (`codigo/[projeto]/`) criada antes da Especificação Técnica existir fisicamente.** Pastas e `git init` foram feitos como "preparação", pulando a fase que deveria ter definido aquela mesma organização de pastas.
3. **Documento de requisitos externo tratado como equivalente ao artefato final da Fase 1**, sem passar pela síntese/reescrita do Agente 1 e sem nunca ser salvo como `documento-requisitos.md`. Pior: isso aconteceu depois de o usuário pedir explicitamente para a sessão **aguardar** antes de prosseguir — pedido que foi ignorado na mesma resposta.

Essas três falhas geraram uma regra nova, transversal a todo o framework, detalhada no `orquestrador.md` deste fork: **Gate de Existência Física entre Fases** + **Regra de Pausa Explícita do Usuário**.

## O que muda por agente (resumo)

- **Agente 1 (Requisitos)**: única fase com conversa humana real, sem mudança de fundo — mas ganhou uma regra nova para o caso de documento de requisitos externo pré-existente (ver arquivo do agente) e uma pergunta final opcional ("quer travar alguma restrição como não-negociável antes do fluxo autônomo assumir?").
- **Agente 2 (Arquiteto)**: decide e documenta com trade-offs explícitos, sem esperar resposta.
- **Agente 3 (Designer)**: decide a direção visual com base no público/contexto dos Requisitos, registrando a justificativa.
- **Agente 4 (Planejador)**: HITL bloqueante deixa de travar — vira AFK Tier 2 obrigatório (decide + cita fonte, ou ADR de decisão nova).
- **Agente 5 (Desenvolvedor)**: aprovação do plano deixa de ser humana, vira self-check formal do Orquestrador.
- **Agentes 6/7 (QA/Revisor)**: **inalterados por completo.**
- **Agente 8 (Documentador)**: inalterado.
- **Orquestrador**: vira o "aprovador em nome do usuário ausente" — ver `orquestrador.md`.

> Nesta entrega (v1.0), **todos os itens do Bloco A do `CRONOGRAMA.md` foram gerados** — os 10 agentes (00 a 09), `orquestrador.md`, `prompt-retomada.md`, os 4 templates, e o `GUIA-DE-INICIO-RAPIDO.md`. Os Agentes 6, 7 e 8 são **cópias intencionais do original, sem mudança de conteúdo** — só ganharam uma nota de fork explicando por quê (ver seção "O que muda por agente" acima: eles não são HITL, são disciplina de processo, e são a rede de segurança técnica que substitui a supervisão humana). Restam só as **2 decisões suas em aberto** (nome definitivo, local do repositório) — ver seção logo abaixo. O comportamento de "Bloqueio Genuíno" já foi decidido e travado (ver item 3 da seção correspondente).

## Agente 9 (novo, exclusivo deste fork): Auditor Externo

Diferente dos agentes 01-08 (que fazem o trabalho), o `agentes/09-auditor-externo.md` é um **prompt de supervisão para uma segunda IA, numa sessão separada**, revisar tudo que o fluxo autônomo produziu e emitir um parecer claro para o humano — sem jargão não traduzido, sem citar um ID sem explicar o que ele significa, terminando sempre com uma recomendação objetiva ("pode prosseguir" / "prossiga com ressalvas" / "recomendo pausar", com o motivo em linguagem direta).

**Por que é uma sessão separada, nunca a mesma que desenvolveu**: o princípio é o mesmo que já existe no framework para QA/Revisor não corrigirem o que eles mesmos estão validando — uma auditoria feita pela mesma IA que gerou o material tende a repetir os próprios pontos cegos. Use com outro modelo/ferramenta quando possível, dando acesso só de leitura.

O agente audita em 4 camadas: (1) existência física real dos artefatos — a mesma causa raiz que originou este fork inteiro; (2) rastreabilidade das decisões em `decisoes-autonomas.md`, reconferindo as fontes citadas, não só aceitando-as; (3) coerência entre os artefatos das diferentes fases; (4) evidência real vs. alegação nas entregas de tarefa (Judge Pass externo).

## Freios que continuam bloqueantes mesmo aqui

Mesmo no modo mais autônomo, o fluxo **para de verdade** (aguardando humano) para:

- Dado real de terceiros, custo financeiro direto, ou ação destrutiva irreversível fora do próprio código.
- Requisito genuinamente ambíguo o bastante para admitir leituras opostas, sem sinal nos Requisitos que decida entre elas.
- Qualquer hard-stop que os agentes já tratam como tal hoje (INTENT gate, teste que contradiz a especificação).
- **Pedido explícito do usuário para pausar** (ex: "aguarde", "não continue ainda") — em qualquer modo, mesmo o mais autônomo. Isso não é uma decisão HITL do fluxo de trabalho — é uma instrução operacional direta sobre o ritmo da conversa.

> **Pergunta em aberto (do prompt original, ainda não respondida por você):** no caso de "requisito genuinamente ambíguo", você prefere que o fluxo realmente pause esperando humano, ou que ele sempre escolha a opção mais conservadora e siga, destacando isso ao máximo em vez de parar? Os arquivos deste fork assumem, por padrão, a opção **pausar de verdade** (a mais conservadora das duas) até você decidir o contrário — ajuste facilmente trocando a seção correspondente em `orquestrador.md` se preferir o outro comportamento.

## Estrutura de arquivos deste fork

```
esquadrao-dev-autonomo/
├── README.md                          (este arquivo)
├── orquestrador.md                    (reescrito — modo autônomo como padrão)
├── prompt-retomada.md                 (reescrito — Gate de Existência Física + pausa em aberto)
├── CHANGELOG.md                       (novo, começa do zero)
├── CRONOGRAMA.md                      (mapa de uso + checklist de construção do fork)
├── GUIA-DE-INICIO-RAPIDO.md           (reescrito — frases-padrão de pausa + uso do Agente 9)
├── agentes/
│   ├── 00-onboarding-legado.md        (reescrito — [INFERIDO] vira Tier 2/ADR nova)
│   ├── 01-analista-requisitos.md      (reescrito — regra de documento externo)
│   ├── 02-arquiteto-software.md       (reescrito — decide e documenta em vez de perguntar)
│   ├── 03-designer-ux-ui.md           (reescrito — direção visual por inferência)
│   ├── 04-planejador-tarefas.md       (reescrito — HITL vira AFK Tier 2 obrigatório)
│   ├── 05-desenvolvedor.md            (reescrito — self-check substitui aprovação humana)
│   ├── 06-qa-testes.md                (cópia intencional, sem mudança de conteúdo)
│   ├── 07-revisor-seguranca.md        (cópia intencional, sem mudança de conteúdo)
│   ├── 08-documentador.md             (cópia intencional, sem mudança de conteúdo)
│   └── 09-auditor-externo.md          (novo — prompt de supervisão por segunda IA)
└── templates/
    ├── decisoes-autonomas.md          (novo — substitui pendencias-revisao.md)
    ├── plano-tarefa.md                (reescrito — self-check formal, sem HITL pendurado)
    ├── estado-projeto.md              (reescrito — Verificação Física + Última Pausa Registrada)
    └── checklist-fases.md             (reescrito — Gate de Existência Física por fase)
```

Todo o Bloco A do `CRONOGRAMA.md` está fechado nesta entrega. As três perguntas do prompt original de especificação seguem em aberto (ver seção abaixo) — os arquivos assumem defaults sinalizados, ajuste quando decidir.

## As 2 decisões suas ainda em aberto

1. **Nome definitivo do fork**: usado "Esquadrão Dev Autônomo" em todo lugar. Troque por find-and-replace se quiser outro nome.
2. **Repositório separado ou pasta alternativa no mesmo repo do Esquadrão Dev original**: os arquivos não assumem nenhum dos dois — funcionam em qualquer lugar, desde que os caminhos internos (`agentes/`, `templates/`) se mantenham relativos à raiz onde este fork estiver.
3. **Comportamento de "Bloqueio Genuíno"**: ✅ **Decidido — o fluxo pausa de verdade**, esperando resposta do usuário, sempre que a ambiguidade for genuína (afeta negócio/experiência do usuário, sem sinal de desempate nos Requisitos nem fonte documental por analogia). Não é mais um default assumido — está travado em `orquestrador.md` ("Freios que continuam bloqueantes"), `templates/decisoes-autonomas.md` (seção "Bloqueios Genuínos") e `templates/plano-tarefa.md` (seção "Exceção que nunca é resolvida sozinha").
# Esquadr-o_Dev_Autonomo
