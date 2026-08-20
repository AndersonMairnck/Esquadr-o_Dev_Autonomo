# Guia de Início Rápido — Esquadrão Dev Autônomo

> Fork do `GUIA-DE-INICIO-RAPIDO.md` original. Para o "porquê" de cada decisão, veja o `README.md` e o `CRONOGRAMA.md` deste fork. Para o comportamento detalhado de cada agente, veja `orquestrador.md` e `agentes/`.

## O que é isso, e a diferença para o Esquadrão Dev original

Mesmos 9+1 "agentes" do original (Requisitos, Arquiteto, Designer, Planejador, Desenvolvedor, QA, Revisor, Documentador, mais o novo Agente 9 — Auditor Externo), coordenados pelo Orquestrador. A diferença: **depois da Fase 1 (Requisitos), o fluxo não pausa esperando sua aprovação em tempo real, a menos que você peça explicitamente.** Toda decisão que no original seria "aprove isso antes de eu continuar" agora é tomada e documentada sozinha em `decisoes-autonomas.md` — você revisa depois, quando quiser, no ritmo que você escolher.

## Pré-requisitos

(Idênticos ao original.) Os arquivos deste fork (`agentes/`, `orquestrador.md`, `prompt-retomada.md`, `templates/`), acesso a uma IA que aceite arquivos longos como instrução, um lugar para salvar arquivos ao longo do processo.

## Como começar

**Se sua IA tem acesso a arquivos** (Claude Code, Cowork, Cursor, Grok Build): peça para ela ler `orquestrador.md` **deste fork** especificamente (não o do Esquadrão Dev original, se os dois estiverem no mesmo lugar) e assumir esse papel:

> "Leia o arquivo `orquestrador.md` deste repositório (Esquadrão Dev Autônomo) e assuma esse papel a partir de agora. Quero um sistema de [...]"

**Se sua IA não tem acesso a arquivos**: cole o conteúdo de `orquestrador.md` deste fork diretamente na primeira mensagem.

## [NOVO] O ponto mais importante deste fork: como controlar até onde ele vai sozinho

Diferente do original (onde o fluxo sempre para nos mesmos pontos fixos: aprovação de plano, direção visual, checkpoint de épico), aqui **você decide onde os freios ficam, a cada vez, pela forma como fraseia o pedido**. Sem nenhuma instrução de pausa, ele tenta ir até o fim sozinho (salvo os poucos freios que continuam bloqueantes por padrão — ver `orquestrador.md`, seção "Freios que continuam bloqueantes").

Frases-padrão úteis (ver `CRONOGRAMA.md`, seção B.1, para mais exemplos):

| O que você quer | Frase |
|---|---|
| Só documentação, revisar antes de qualquer código | "Inicie o fluxo, gere toda a documentação inicial e aguarde eu autorizar o desenvolvimento." |
| Um épico específico, depois revisar | "Desenvolva o Épico 1 todo e pare quando tiver tudo pronto." |
| Sem pausa nenhuma | "Construa o sistema completo, sem pausar entre fases." |
| Retomar após ajuste, sem soltar de vez | "Ajuste [X] e volte a aguardar." |

**Se você não disser nada equivalente a "aguarde" ou "pare quando", ele não vai parar sozinho em nenhuma fronteira de fase.** Isso é intencional — é a autonomia real que o fork existe para entregar — mas significa que colocar os freios é responsabilidade sua, a cada sessão.

## [NOVO] Usando o Agente 9 — Auditor Externo

A qualquer pausa (documentação pronta, épico pronto, ou quando quiser), você pode pedir uma segunda opinião independente:

1. Abra uma conversa **separada** (idealmente outro modelo/ferramenta).
2. Cole `agentes/09-auditor-externo.md`.
3. Dê acesso **só de leitura** aos artefatos do projeto.
4. Peça: "audite tudo que já foi produzido" (ou delimite uma fase/tarefa específica).
5. Você recebe um Parecer de Auditoria com uma recomendação clara: prosseguir sem ressalvas / prosseguir com ressalvas / recomendo pausar — sem jargão não explicado, sem IDs soltos.

Use isso especialmente em marcos importantes: fim da documentação inicial, fim de épicos grandes, antes da entrega final. Nunca use a mesma sessão que desenvolveu para se auto-auditar — o valor está na independência.

## O que esperar de você ao longo do processo

Diferente do original (onde pontos fixos exigem sua palavra), aqui **nada exige sua palavra por padrão** — exceto:
- A conversa de Requisitos (Fase 1), sempre humana.
- Qualquer ponto onde você pediu pausa explicitamente.
- **Bloqueios Genuínos**: ambiguidade real de requisito sem sinal de desempate, dado real de terceiros/custo financeiro direto, ação destrutiva irreversível fora do código, hard-stops técnicos já existentes (INTENT gate, teste que contradiz especificação).

## Se algo travar ou você preferir controlar cada fase manualmente

(Idêntico ao original — pode rodar cada agente manualmente, colando um de cada vez.) Note que, mesmo manualmente, os agentes 02-05 deste fork não vão pausar pedindo sua aprovação — eles decidem e documentam. Se você quer o comportamento síncrono clássico (aprovar cada decisão na hora), use o Esquadrão Dev original, não este fork.

## Retomando em uma sessão nova

(Idêntico ao original no mecanismo — cole `prompt-retomada.md` deste fork.) **[NOVO]** Diferente do original, a sessão nova primeiro checa se havia uma pausa em aberto (passo 1.5 do `prompt-retomada.md` deste fork) antes de fazer qualquer outra coisa — se você tinha pedido "aguarde" e nunca autorizou, a sessão nova respeita isso também, não retoma sozinha só porque é uma conversa nova.

## Se o sistema já existe (não é um projeto novo)

(Idêntico ao original — use `agentes/00-onboarding-legado.md` deste fork primeiro.)

## Erros comuns a evitar (específicos deste fork, além dos do original)

- **Assumir que "sem pausa pedida" significa "sem controle nenhum".** Você sempre pode auditar depois via `decisoes-autonomas.md` ou pedir uma auditoria externa (Agente 9) — não é irreversível, só é assíncrono.
- **Confundir "o agente disse que ia criar" com "o agente criou".** Se você notar qualquer artefato citado que parece não existir, peça: "rode a verificação física de tudo até agora" — isso força o Gate de Existência Física a rodar sob demanda.
- **Deixar uma pausa em aberto sem retomar por muito tempo e depois abrir uma sessão nova esperando que ela "lembre" a pausa sem reler os arquivos.** Sempre use `prompt-retomada.md` deste fork ao voltar — nunca só "continue" sem contexto.
- **Auditar com a mesma sessão que desenvolveu.** Perde o valor da segunda opinião — use sessão separada para o Agente 9.
