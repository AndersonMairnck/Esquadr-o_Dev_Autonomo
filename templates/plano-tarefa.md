# Plano — Tarefa [ID / Nome da Tarefa] (Modo Autônomo)

> Copie para `planos/tarefa-[ID].md` ao apresentar o plano de uma tarefa nova. Fork do `plano-tarefa.md` original — a diferença de fundo: a tabela de Classificação da Decisão nunca deixa uma linha "HITL bloqueante, não resolvida" pendurada esperando humano. Toda decisão sempre chega a uma resolução (Tier 2 com fonte, ou ADR nova) antes deste plano poder ser autoaprovado.

**Status deste plano:** Em elaboração / Plano autoaprovado em [data], checklist 3/3 / Ajustado em [data]

> A linha "Plano autoaprovado em [data], checklist 3/3" só pode ser escrita depois do self-check formal descrito em `agentes/05-desenvolvedor.md` deste fork: Teste do Júnior sem Discernimento confirmado + Checklist Objetivo de Clareza 7/7 + nenhuma decisão desta tabela sem Tier 2/fonte ou ADR nova. Nunca escreva essa linha antes dos três estarem de fato confirmados.

## Camada
Backend / Frontend / Full-stack / Infra

## Arestas de bloqueio
- **Bloqueada por**: [ID de outra tarefa, ou "nenhuma"]
- **Bloqueia**: [ID de outra tarefa, ou "nenhuma"]

## O que será criado/alterado
| Arquivo | Ação (criar/alterar) | Descrição |
|---------|------------------------|-----------|

## Abordagem
[Como a tarefa será resolvida, em linguagem simples]

## Seams de teste acordados
[Fronteira onde o teste vai verificar o comportamento — combine agora, não durante a implementação]

## Decisões de design não óbvias
[Toda escolha que não é a única opção razoável, com justificativa. Toda decisão aqui precisa aparecer também na tabela abaixo, classificada]

## Classificação da Decisão — Modo Autônomo (nunca fica "pendente de humano")

Use o mesmo critério objetivo de 3 condições do framework original para **identificar** o peso da decisão — mas neste fork, identificar como "seria HITL" nunca trava o plano, só determina o caminho de resolução:

1. **Difícil de reverter**
2. **Sem precedente documental**
3. **Trade-off real de negócio ou técnico com impacto observável**

Se as três forem verdadeiras: procure precedente primeiro (`plano de tarefa anterior do mesmo módulo → decisoes-autonomas.md → contrato → especificação técnica → documento de requisitos`, incluindo a seção 7 de restrições travadas). Se achar, resolve como **Tier 2** citando a fonte. Se não achar, resolve como **ADR de decisão nova** — escolha a alternativa mais conservadora/reversível entre as razoáveis, registre em `decisoes-autonomas.md` com alternativas descartadas e motivo.

Se qualquer uma das três condições faltar, é **AFK Tier 1** — baixo risco, segue silencioso.

**Exceção que nunca é resolvida sozinha, mesmo aqui — "Bloqueio Genuíno":** se a decisão é uma ambiguidade genuína de requisito/regra de negócio que admite leituras opostas, **sem nenhum sinal nos artefatos que decida entre elas** (nem mesmo por analogia fraca), isso não vira Tier 2 nem ADR nova — vira uma linha em "Perguntas em aberto para o usuário" (seção abaixo) e, dependendo da configuração do `orquestrador.md` deste fork, pode pausar de verdade o fluxo. Não force uma decisão só para preencher a tabela quando a ambiguidade for real.

| Decisão | Peso (3 condições?) | Resolução (Tier 1 / Tier 2 / ADR nova / Bloqueio Genuíno) | Fonte citada (Tier 2) ou Alternativas descartadas (ADR nova) | ID em decisoes-autonomas.md |
|---------|---------------------------|------------------------------------------------------------------|-------------------------------------------------------------------|-----------------------------------|

**Se esta tarefa não tem nenhuma decisão de design não óbvia**, escreva apenas "Nenhuma decisão relevante nesta tarefa" — não preencha a tabela vazia.

## Teste do júnior sem discernimento
[Esse plano é claro o bastante para alguém sem contexto do projeto seguir sem inventar nada? Se não, o que falta detalhar?]

## Checklist Objetivo de Clareza (herdado do Agente 4 — confirme os 7 itens antes do self-check)
- [ ] Especifica quais arquivos devem ser criados/modificados?
- [ ] Especifica quais funções/métodos/endpoints devem existir?
- [ ] Especifica quais parâmetros/inputs cada função ou endpoint recebe?
- [ ] Especifica o que deve ser retornado em caso de sucesso?
- [ ] Especifica o que deve ser retornado/lançado em caso de erro?
- [ ] Especifica quais dependências/bibliotecas novas são necessárias (se houver)?
- [ ] Especifica como testar manualmente a funcionalidade?

## Dependências e pré-requisitos
[O que precisa já existir/estar pronto]

## Perguntas em aberto para o usuário (só Bloqueio Genuíno, neste fork)
[Diferente do original, esta seção deveria estar vazia na maioria das tarefas — só é preenchida quando a "Exceção" da tabela acima foi de fato acionada. Uma seção vazia aqui é o comportamento esperado e correto, não um sinal de tarefa incompleta.]

---

## Self-check formal (preencher antes de mudar o Status para "autoaprovado")
- [ ] Teste do Júnior sem Discernimento: confirmado
- [ ] Checklist Objetivo de Clareza: 7/7
- [ ] Tabela de Classificação da Decisão: nenhuma linha sem Tier/ADR/Bloqueio Genuíno explícito — nenhuma decisão "esquecida" sem resolução
- [ ] Nenhuma pausa explícita do usuário está ativa nesta sessão (ver regra de topo do orquestrador.md deste fork) — se estiver, este plano fica em "Em elaboração", nunca autoaprovado, até a pausa ser resolvida

## Ajustes durante a implementação
_(Se algo mudou depois da autoaprovação, registre aqui: o que mudou, quando, por quê — não edite as seções acima retroativamente)_
