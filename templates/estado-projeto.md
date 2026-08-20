# Estado do Projeto — [Nome do Sistema] (Modo Autônomo)

> Fork do `estado-projeto.md` original. Cole este arquivo (ou as seções relevantes) como contexto inicial de qualquer nova conversa com um agente. Diferença de fundo: este arquivo agora referencia também `decisoes-autonomas.md`, e todo campo "Status: Concluída" só pode ser preenchido depois de verificação física direta do artefato correspondente (ver Gate de Existência Física em `orquestrador.md`) — nunca com base em "foi dito na resposta anterior".

## Caminhos deste projeto

- **Acompanhamento do processo**: `projetos/[nome-do-projeto]/`
- **Código-fonte real**: `codigo/[nome-do-projeto]/backend` e `codigo/[nome-do-projeto]/frontend`
- **Contratos de API Backend → Frontend**: `projetos/[nome-do-projeto]/contratos/modulo-[nome].md`
- **[NOVO] Log de decisões autônomas**: `projetos/[nome-do-projeto]/decisoes-autonomas.md` — leia junto com este arquivo sempre; é tão essencial quanto este para entender o estado real do projeto.

## Status Geral

| Fase | Status | Data | Verificação Física Confirmada? [NOVO] |
|------|--------|------|-------------------------------------------|
| 1. Requisitos | Não iniciado / Em andamento / Concluído | | Sim/Não — artefato: `documento-requisitos.md` |
| 2. Arquitetura | Não iniciado / Em andamento / Concluído | | Sim/Não — artefato: `especificacao-tecnica.md` |
| 3. Design UX/UI | Não iniciado / Em andamento / Concluído | | Sim/Não — artefato: `design-ux-ui.md` |
| 4. Planejamento | Não iniciado / Em andamento / Concluído | | Sim/Não — artefato: `backlog.md` |
| 5-7. Dev/QA/Revisão | Não iniciado / Em andamento / Concluído | | Sim/Não — por tarefa, ver seção 5-7 |
| 8. Documentação | Não iniciado / Em andamento / Concluído | | Sim/Não — artefato: `documentacao/` |

> **Nunca marque "Concluído" na coluna Status sem preencher "Sim" na coluna de Verificação Física, com o artefato de fato lido e confirmado nesta mesma sessão.** Esta é a correção direta do erro que originou este fork: uma fase sendo declarada pronta porque "foi gerada na resposta anterior", sem confirmação real de que o arquivo existe no disco.

---

## 1. Documento de Requisitos
Não cole aqui — referencie `documento-requisitos.md`. **[NOVO]** Se este documento foi sintetizado a partir de um arquivo externo trazido pelo usuário, registre aqui a origem (ver seção 11 do formato de saída do Agente 1 deste fork).

---

## 2. Especificação Técnica
Não cole aqui — referencie `especificacao-tecnica.md` (+ módulos se 4+). **[NOVO]** Confirme aqui que a seção "Rastreabilidade das Decisões Autônomas" (seção 13 do Agente 2 deste fork) está preenchida.

---

## 3. Design de UX/UI
Não cole aqui — referencie `design-ux-ui.md` (+ módulos se 4+). **[AJUSTADO]** Confirme aqui que a direção visual foi **decidida por inferência documentada** (não mais "validada com o usuário" — ver Agente 3 deste fork) e que a seção de Rastreabilidade está preenchida.

---

## 4. Backlog de Tarefas
Não cole aqui — referencie `backlog.md`. **[NOVO]** Confirme que nenhuma tarefa ficou com decisão HITL não resolvida (ver critério de "pronto" do Agente 4 deste fork) — toda decisão deveria estar em Tier 2/ADR nova, salvo Bloqueio Genuíno explícito.

---

## 5-7. Entregas de Tarefas (Dev → QA → Revisão)

### Painel por Camada (Backend / Frontend / Full-stack / Infra)
(Idêntico ao original — índice de leitura rápida por camada.)

**Backend**
| Tarefa | Módulo | Status | Resumo de 1 linha |
|--------|--------|--------|----------------------|

**Frontend**
| Tarefa | Módulo | Status | Resumo de 1 linha |
|--------|--------|--------|----------------------|

**Full-stack / Infra**
| Tarefa | Módulo | Status | Resumo de 1 linha |
|--------|--------|--------|----------------------|

---

### Tarefa [ID]
- **Camada**: Backend / Frontend / Full-stack / Infra
- **Módulo**: _(mesmo nome de épico do backlog)_
- **Status**: Não iniciada / Plano em elaboração / **Plano autoaprovado** [NOVO — substitui "Aprovada para código"] / Em desenvolvimento / Em QA / Em revisão / Concluída
- **Plano**: `planos/tarefa-[ID].md`
- **Entrega (Dev + QA + Revisão)**: `entregas/tarefa-[ID].md`
- **Resumo de 1 linha**: _(ex: "Concluída — 424/424 testes, RLS comprovado, autoaprovado em 20/08")_
- **[NOVO] Decisões autônomas desta tarefa**: [IDs em decisoes-autonomas.md, se houver — ou "nenhuma decisão não óbvia nesta tarefa"]

_(Repita este bloco para cada tarefa do backlog)_

---

## 8. Documentação Final
Não cole aqui — referencie `documentacao/`.

---

## Decisões Pendentes de Validação Humana
**[AJUSTADO — MODO AUTÔNOMO]** Neste fork, esta seção só deveria conter itens de **Bloqueio Genuíno** (ver `orquestrador.md`) — qualquer decisão que no framework original seria HITL "comum" já foi resolvida e está em `decisoes-autonomas.md`, não aqui. Se você encontrar algo nesta tabela que não é um Bloqueio Genuíno de verdade, isso é sinal de que uma decisão foi deixada pendente por engano — trate como um problema a corrigir, não como estado normal.

| ID | O que está pendente | Origem (tarefa/épico/agente) |
|----|------------------------|----------------------------------|

## Dívida Técnica / Bloqueios Não Resolvidos
(Idêntico ao original — problema técnico real contornado/adiado/não resolvido, com ID sequencial P01, P02...)

| ID | Tarefa | O que ficou pendente | Risco se não resolver |
|----|--------|------------------------|--------------------------|

## Histórico de Mudanças de Escopo
(Idêntico ao original.)

## [NOVO — MODO AUTÔNOMO] Última Pausa Registrada
_(Preencha sempre que o usuário der uma instrução de pausa — ex: "aguarde autorização". Isso é o que permite a uma sessão nova, ao retomar via prompt-retomada.md, saber se pode prosseguir automaticamente ou se precisa esperar decisão do usuário antes de qualquer coisa.)_

- **Instrução de pausa dada em**: [data/hora, se souber]
- **Texto da instrução**: [ex: "gere toda a documentação inicial e aguarde eu autorizar o desenvolvimento"]
- **Ainda ativa?**: Sim / Não — resolvida em [data], autorização: [o que o usuário disse]
