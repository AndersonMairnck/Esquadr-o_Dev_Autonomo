# Decisões Autônomas — [Nome do Sistema]

> Copie para `projetos/[nome-do-projeto]/decisoes-autonomas.md`. Substitui, no modo autônomo, tanto a tabela "Decisões Pendentes de Validação Humana" quanto a "Classificação HITL/AFK" do plano — toda decisão que seria uma dessas categorias no framework original vira uma entrada aqui, **já resolvida**, não pendente. É um **log permanente e cumulativo** do projeto — nunca zere ou apague uma entrada antiga, mesmo que ela pareça "resolvida e sem importância" depois.
>
> Não duplique o conteúdo do plano/entrega aqui — só a decisão em si e a fonte, com link para o arquivo completo (mesmo padrão já usado entre `estado-projeto.md` e `planos/`/`entregas/`).

## Como preencher cada entrada

| Campo | Conteúdo |
|-------|----------|
| ID | Sequencial, ex: DA-001 |
| Fase/Agente | Qual agente tomou a decisão |
| O que foi decidido | Objetivo, sem jargão |
| Fonte usada | `plano > contrato > spec > requisitos` (citar qual e onde) — ou "sem precedente — decisão nova" |
| Alternativas descartadas | E por quê |
| Reversibilidade | Fácil / Difícil — decisões difíceis de reverter merecem uma linha a mais de justificativa |
| Épico/Tarefa | Para navegação |

**Antes de registrar qualquer decisão como Tier 2 (com fonte), confirme que a fonte citada realmente resolve a decisão por analogia direta** — uma fonte genérica demais que "poderia" se aplicar não é a mesma coisa que uma fonte que resolve especificamente. Se a fonte for fraca demais para sustentar a decisão sozinha, trate como "sem precedente — decisão nova" em vez de forçar uma citação Tier 2 artificial.

---

## Log de Decisões

### DA-001
- **Fase/Agente**:
- **O que foi decidido**:
- **Fonte usada**:
- **Alternativas descartadas**:
- **Reversibilidade**: Fácil / Difícil
- **Épico/Tarefa**:

<!-- Repita o bloco acima para cada nova decisão, sempre incrementando o ID sequencialmente. -->

---

## Bloqueios Genuínos (freio que continuou parando o fluxo)

> Diferente do log acima — aqui vão só os casos em que nenhuma fonte resolvia a decisão por analogia **e** a ambiguidade era genuína o bastante para admitir leituras opostas, então o fluxo parou de verdade esperando humano (ver "Freios que continuam bloqueantes" no `orquestrador.md`). Se o seu projeto decidiu trocar esse comportamento por "segue com a opção conservadora e destaca" em vez de pausar, registre aqui do mesmo jeito — a diferença é só se o fluxo esperou ou seguiu.

| ID | O que travou | Leitura conservadora adotada (se não pausou) | Status |
|----|-----------------|--------------------------------------------------|--------|

---

## Fechamento por Épico (ponto de corte de leitura)

> A cada épico concluído, feche um bloco aqui — não é uma pausa do fluxo, é só um marcador para permitir que uma revisão humana futura leia por partes em vez de ter que varrer o log inteiro de uma vez.

### Épico [N] — [nome] — fechado em [data]
- Decisões deste épico: DA-XXX a DA-YYY
- Resumo de 1 linha do estado ao fechar: [ex: "todas as tarefas concluídas, QA de integração do épico passou, nenhuma pendência aberta"]
