# Checklist de Critérios de "Pronto" por Fase — Modo Autônomo

> Fork do `checklist-fases.md` original. Regra transversal ajustada:

> **NUNCA marque uma tarefa/fase concluída no estado-projeto.md sem, no mesmo momento, ter (1) rodado build+testes reais e conferido o resultado, quando aplicável, E (2) confirmado por leitura direta que o artefato correspondente existe fisicamente no disco.** "Parece pronto", "eu disse que ia criar" e "está pronto" são três coisas diferentes — a diferença é sempre uma verificação real, não uma narração.

## Fase 1 — Requisitos (Agente 1)
- [ ] Todo requisito funcional tem critério de aceite testável
- [ ] Não há contradições entre requisitos
- [ ] Prioridades (essencial vs. desejável) estão definidas
- [ ] Volume esperado de uso foi estimado
- [ ] Não há pendências críticas em aberto
- [ ] **[NOVO]** Se havia documento externo pré-existente, ele foi checado contra este checklist e sintetizado — não usado como substituto do artefato final
- [ ] **[NOVO]** A pergunta de "restrição não-negociável para as fases seguintes" foi feita e registrada
- [ ] **[NOVO]** `documento-requisitos.md` existe fisicamente, confirmado por leitura direta

## Fase 2 — Arquitetura (Agente 2)
- [ ] Toda funcionalidade essencial tem endereçamento arquitetural
- [ ] Todo RF aparece na tabela de Cobertura de Requisitos, sem "Não" sem justificativa
- [ ] Todo RNF aparece na tabela de Mapeamento de RNFs com decisão técnica associada
- [ ] Stack está justificada
- [ ] Modelo de dados cobre todas as entidades dos requisitos
- [ ] Riscos técnicos relevantes identificados com mitigação
- [ ] **[AJUSTADO]** Trade-offs importantes foram decididos e documentados em `decisoes-autonomas.md` (não mais "validados com o usuário")
- [ ] Toda ADR registrada atende aos 3 critérios simultâneos (difícil de reverter + surpreendente sem contexto + trade-off real)
- [ ] **[NOVO]** A seção 13 (Rastreabilidade das Decisões Autônomas) está preenchida
- [ ] **[NOVO]** `especificacao-tecnica.md` (+ módulos se 4+) existe fisicamente, confirmado por leitura direta

## Fase 3 — Design UX/UI (Agente 3)
- [ ] **[AJUSTADO]** A direção visual foi decidida por inferência documentada do público/contexto dos Requisitos — nunca assumida sem justificativa nem copiada de projeto anterior
- [ ] Existe Design System mínimo documentado
- [ ] Todo padrão de componente reutilizável está definido uma única vez
- [ ] Responsividade tratada explicitamente para cada padrão de componente
- [ ] Toda tela essencial dos requisitos tem fluxo de navegação correspondente
- [ ] **[NOVO]** A seção de Rastreabilidade das Decisões Autônomas está preenchida
- [ ] **[NOVO]** `design-ux-ui.md` (+ módulos se 4+) existe fisicamente, confirmado por leitura direta

## Fase 4 — Planejamento (Agente 4)
- [ ] Toda funcionalidade essencial está coberta por ao menos uma tarefa
- [ ] Cada tarefa tem critério de aceite claro
- [ ] Tarefas de Frontend referenciam o padrão de componente correspondente do Design de UX/UI
- [ ] Arestas de bloqueio mapeadas nos dois sentidos
- [ ] Toda tarefa corta fatia vertical demonstrável, exceto expand-contract marcado
- [ ] **[AJUSTADO]** Toda decisão que seria HITL no original está resolvida como Tier 2 (fonte citada) ou ADR nova — nenhuma tarefa fica bloqueada por "aprovação humana pendente"
- [ ] **[NOVO]** "Perguntas em aberto para o usuário" só contém Bloqueios Genuínos reais
- [ ] Nenhuma tarefa é vaga demais (Teste do Júnior)
- [ ] Checklist Objetivo de Clareza (7 itens) marcado "Sim" para cada tarefa
- [ ] **[NOVO]** `backlog.md` existe fisicamente, confirmado por leitura direta

## Fase 5 — Desenvolvimento (Agente 5) — por tarefa
- [ ] **[AJUSTADO]** O plano da tarefa tem a linha "Plano autoaprovado em [data], checklist 3/3" — não mais "aprovação explícita do usuário"
- [ ] Critério de aceite da tarefa 100% atendido
- [ ] Teste do happy path escrito antes do código correspondente
- [ ] Testes unitários escritos cobrindo happy path, bordas e erros, no seam acordado
- [ ] Código aderente à stack e padrões definidos
- [ ] Tarefas de Frontend seguem o Design de UX/UI
- [ ] Nenhum dado sensível exposto no código
- [ ] **[AJUSTADO]** Toda decisão que seria HITL do plano está resolvida (Tier 2/ADR nova), nunca "decidida informalmente" sem registro em `decisoes-autonomas.md`
- [ ] Se for correção de bug: existe teste de regressão que reproduz a falha original
- [ ] **[NOVO]** `entregas/tarefa-[ID].md` existe fisicamente com a seção do Desenvolvedor preenchida, confirmado por leitura direta

## Fase 6 — QA (Agente 6) — por tarefa
(Idêntico ao original — sem alteração de conteúdo, ver nota de fork no próprio `agentes/06-qa-testes.md`.)
- [ ] Todo critério de aceite verificado individualmente
- [ ] Casos de borda relevantes testados
- [ ] Nenhum problema Crítico ou Alto sem resposta
- [ ] Testes de integração escritos quando necessário
- [ ] Teste de Não Regressão rodado e nenhum teste anterior quebrou
- [ ] Se correção de bug: teste de reprodução confirmado antes de aprovar
- [ ] Nenhum bug encontrado pelo QA foi corrigido por ele mesmo — sempre devolvido ao Agente 5

## Fase 7 — Revisão (Agente 7) — por tarefa
(Idêntico ao original — sem alteração de conteúdo.)
- [ ] Nenhuma vulnerabilidade de segurança relevante em aberto
- [ ] Eixo A e Eixo B avaliados separadamente, Eixo B como cross-check sobre QA
- [ ] Código aderente aos padrões e arquitetura
- [ ] Sem problemas de performance previsíveis
- [ ] Tarefas de Frontend aderentes ao Design System
- [ ] Ressalvas não-bloqueantes documentadas
- [ ] Nenhum problema encontrado pelo Revisor foi corrigido por ele mesmo

## Fase 8 — Documentação (Agente 8)
(Idêntico ao original.)
- [ ] Alguém sem contexto consegue instalar e rodar o sistema pelo README
- [ ] Decisões de arquitetura registradas com o "porquê"
- [ ] Toda API documentada com exemplos reais
- [ ] Toda API tem "Códigos de Erro Comuns" preenchida com erros reais
- [ ] Documentação reflete o sistema como foi de fato implementado
- [ ] **[NOVO]** `documentacao/` existe fisicamente, confirmado por leitura direta

## Checkpoint de Épico (Orquestrador) — antes de avançar para o próximo épico
- [ ] QA rodou testes de integração cobrindo o épico inteiro
- [ ] Revisor confirmou coesão arquitetural entre as tarefas do épico
- [ ] `estado-projeto.md` foi atualizado refletindo o épico concluído
- [ ] **[AJUSTADO]** Bloco de fechamento do épico registrado em `decisoes-autonomas.md` — substitui o "pode seguir" do usuário como condição de avanço, salvo se o usuário tiver pedido pausa explícita neste ponto

## Gate de Cobertura (Orquestrador) — antes de declarar "pronto para entrega final"
- [ ] Todo RF marcado Essencial tem uma tarefa Concluída cujo critério de aceite realmente o satisfaz
- [ ] Todo RNF marcado Essencial tem uma tarefa Concluída cujo critério de aceite realmente o satisfaz
- [ ] Se algum RF/RNF Essencial não tiver entrega real correspondente, isso foi sinalizado e um épico novo foi criado
- [ ] **[NOVO]** Nenhuma pausa explícita do usuário está ativa e não resolvida (ver `estado-projeto.md`, seção "Última Pausa Registrada") antes de declarar o projeto pronto

## [NOVO — MODO AUTÔNOMO] Gate de Existência Física — aplicável a toda fase acima
- [ ] O artefato desta fase foi lido diretamente do disco nesta mesma sessão antes de marcar "Concluída" — nunca inferido de resposta anterior
- [ ] Nenhum artefato de fase posterior (incluindo estrutura de `codigo/[projeto]/`) foi criado antes deste artefato existir fisicamente
