# Changelog — Esquadrão Dev Autônomo

> Projeto novo, changelog começa do zero — não é uma versão do Esquadrão Dev original.

## v0.1 — Primeira entrega do fork

### Adicionado: `orquestrador.md` (fork) com modo autônomo como padrão

- Seção **"Regra de topo: pedido explícito de pausa do usuário é sempre respeitado"** — corrige uma falha real observada: uma sessão declarou "aguardando instruções" e, na mesma resposta, prosseguiu para a fase seguinte sem nova mensagem do usuário.
- Seção **"Gate de Existência Física entre Fases"** — corrige duas falhas reais observadas: (1) fases declaradas "concluídas" no Formato de Status sem o artefato existir de fato no disco; (2) estrutura de código e `git init` criados como "preparação" antes da Especificação Técnica existir fisicamente, mesmo essa estrutura sendo, ela mesma, uma decisão que pertence à Especificação Técnica (seção 3.1).
- Seção **"Documento de requisitos externo pré-existente não é o artefato final da Fase 1"** — corrige uma terceira falha observada: um arquivo de requisitos trazido de fora do framework foi tratado como equivalente ao artefato final da Fase 1, sem nunca passar pela síntese/checklist/salvamento formal do Agente 1.
- Seção **"O Orquestrador como aprovador em nome do usuário ausente"** — promove a seção "Execução autônoma sem supervisão em tempo real" do original de exceção condicional a modo padrão, removendo o teto de "1 épico sem checagem" como pausa obrigatória (vira só ponto de corte de leitura em `decisoes-autonomas.md`).
- Seção **"Freios que continuam bloqueantes"** — lista o que ainda para de verdade mesmo neste modo (dado real de terceiros/custo financeiro/ação destrutiva irreversível; ambiguidade genuína sem sinal nos Requisitos; hard-stops já existentes nos agentes; pedido explícito de pausa).
- **Formato de Status ajustado** com campo novo obrigatório `VERIFICAÇÃO FÍSICA`, exigindo que toda alegação de "Concluída" venha acompanhada da confirmação de leitura direta do artefato em disco.
- Demais seções (gate de `estado-projeto.md`, Checagem de fechamento, Judge pass, regras de QA/Revisor, Modo de Planejamento em Lote, Disciplina de escrita em arquivos de estado) herdadas do `orquestrador.md` original sem alteração de fundo — resumidas por referência neste fork.

### Adicionado: `agentes/01-analista-requisitos.md` (fork)

- Regra nova: **documento de requisitos externo pré-existente exige leitura + checklist de "pronto" aplicado contra ele + síntese e salvamento formal em `documento-requisitos.md`** antes de a Fase 1 ser considerada concluída — nunca tratar o arquivo externo, sozinho, como o artefato final.
- Reforço explícito de que um pedido de pausa do usuário durante a leitura do documento externo deve ser respeitado de fato, sem emendar para a fase seguinte na mesma resposta.
- Nova pergunta final de entrevista: "há alguma restrição que você quer travada como não-negociável para as fases seguintes?" — única janela de intenção antes do fluxo autônomo assumir.
- Nova seção 11 no formato de saída ("Fonte deste documento"), para rastrear se o requisito veio de arquivo externo ou foi levantado do zero na conversa.

### Adicionado: `templates/decisoes-autonomas.md`

- Novo artefato, renomeando conceitualmente `entregas/pendencias-revisao.md` do original — tratado como log permanente e cumulativo, não uma fila a ser zerada. Inclui seção de "Bloqueios Genuínos" e "Fechamento por Épico" como ponto de corte de leitura.

### Pendente para próximas entregas

- Agentes 02 a 08 ainda não foram reescritos para este fork — herdam o comportamento HITL do Esquadrão Dev original por enquanto (ver `README.md`, seção "O que muda por agente", para o resumo do que cada um precisa ganhar).
- `prompt-retomada.md` do fork ainda não foi ajustado para incluir `decisoes-autonomas.md` como camada de consulta na ordem de precedência (item 4 do "O que o novo projeto deve entregar", no prompt original desta especificação).
- Três perguntas do prompt original seguem em aberto e foram respondidas com defaults neste v0.1, sinalizados no `README.md`: nome definitivo do fork, repositório separado vs. pasta alternativa no mesmo repo, e se "Bloqueio genuíno" deve pausar de verdade (default adotado) ou sempre seguir com a opção conservadora sem pausar.

## v0.2 — Agentes 4, 5, cópias 6-8, e Agente 9 (Auditor Externo)

### Adicionado: `agentes/04-planejador-tarefas.md` (fork)

- Classificação HITL bloqueante do original deixa de travar a liberação da tarefa: toda decisão que seria HITL agora é resolvida como AFK Tier 2 (com fonte citada) ou ADR de decisão nova, seguindo a mesma ordem de precedência documental já usada no Agente 2 e no `orquestrador.md`.
- A tabela "Perguntas em aberto para o usuário" do plano só é preenchida em caso de Bloqueio Genuíno real — nunca para decisões já resolvidas pelo agente.
- Nova seção "Rastreabilidade das Decisões Autônomas" ao final do Backlog.

### Adicionado: `agentes/05-desenvolvedor.md` (fork)

- A "Trava obrigatória" do original (aprovação humana explícita do plano antes de codificar) é substituída por um self-check formal em 3 pontos (Teste do Júnior sem Discernimento, Checklist Objetivo de Clareza, tabela de decisões resolvida) — registrado explicitamente em `planos/tarefa-[ID].md` como "Plano autoaprovado em [data], checklist 3/3".
- Reforço explícito: o self-check nunca sobrepõe um pedido de pausa já dado pelo usuário na sessão — a regra de topo do `orquestrador.md` continua tendo prioridade máxima.
- Toda a disciplina técnica do original (Diagnóstico Disciplinado de Bugs, TDD do happy path, Contrato Backend/Frontend, INTENT gate, resolução de merge/rebase) mantida sem alteração de conteúdo.

### Adicionado: `agentes/06-qa-testes.md`, `07-revisor-seguranca.md`, `08-documentador.md` (fork)

- Cópias intencionais, **sem nenhuma mudança de conteúdo** em relação ao Esquadrão Dev original — só ganharam uma nota de fork explicando o porquê: as regras duras de QA/Revisor não são HITL, são disciplina de processo, e são a rede de segurança técnica que substitui a supervisão humana em tempo real neste fork.

### Adicionado: `agentes/09-auditor-externo.md` — novo, exclusivo deste fork

- **Motivação**: testes reais mostraram que uma segunda IA, numa sessão separada da que desenvolve, consegue revisar as documentações e o código gerado e sinalizar problemas de forma útil — faltava um prompt padronizado para isso, com formato de saída pensado para um humano não-técnico no mesmo nível dos agentes conseguir ler e decidir.
- Audita em 4 camadas: (1) existência física real dos artefatos; (2) rastreabilidade das decisões em `decisoes-autonomas.md`, reconferindo as fontes citadas em vez de só aceitá-las; (3) coerência entre artefatos de diferentes fases; (4) evidência real vs. alegação nas entregas de tarefa (Judge Pass externo).
- Desenhado para ser usado **sempre numa sessão separada** da que desenvolveu, de preferência com outro modelo/ferramenta — mesmo princípio de independência que já existe entre QA/Revisor e o código que eles validam, aplicado um nível acima.
- Formato de saída força tradução de severidade técnica para impacto prático, proíbe citar ID sem explicar o significado, e termina sempre com uma de três recomendações objetivas: prosseguir sem ressalvas / prosseguir com ressalvas / recomendo pausar.
- É somente leitura por design — nunca corrige nada, só reporta.

### Atualizado: `README.md` e `CRONOGRAMA.md`

- Refletem os 8 agentes + Agente 9 já gerados; `CRONOGRAMA.md` ganhou a subseção "Bloco A.1 — Como usar o Agente 9 na prática", encaixando a auditoria externa como um passo opcional a cada pausa do Bloco B.

### Pendente para próximas entregas

- `prompt-retomada.md`, `templates/plano-tarefa.md`, `templates/estado-projeto.md`, `templates/checklist-fases.md`, `GUIA-DE-INICIO-RAPIDO.md` e `agentes/00-onboarding-legado.md` ainda não foram adaptados — ver `CRONOGRAMA.md`, Bloco A.
- As mesmas três perguntas em aberto do v0.1 continuam sem confirmação sua.

## v1.0 — Fork completo: prompt-retomada, templates, guia, onboarding legado

### Adicionado: `prompt-retomada.md` (fork)

- Novo passo 1.5: verifica se há uma pausa em aberto (instrução do usuário) antes de qualquer outra coisa — retomar sessão não é autorização implícita para prosseguir além de uma pausa pedida.
- Novo passo 2.4: verifica a existência física real de tudo que `estado-projeto.md` alega, nunca confiando na narração de sessões anteriores — se encontrar divergência, registra o incidente e reconstrói retroativamente antes de continuar.
- Ordem de precedência do passo 2.7 ganha uma camada nova: `decisoes-autonomas.md` entra entre o plano da tarefa e o contrato.
- Formato de diagnóstico final ganha os campos "VERIFICAÇÃO FÍSICA REALIZADA" e "PAUSA EM ABERTO".

### Adicionado: `templates/plano-tarefa.md`, `templates/estado-projeto.md`, `templates/checklist-fases.md` (fork)

- `plano-tarefa.md`: a tabela de Classificação da Decisão nunca deixa uma linha HITL pendurada — toda decisão sempre chega a Tier 1/Tier 2/ADR nova/Bloqueio Genuíno. A linha "Plano autoaprovado" substitui a aprovação humana, condicionada ao self-check formal.
- `estado-projeto.md`: nova coluna "Verificação Física Confirmada?" na tabela de Status Geral; nova seção "Última Pausa Registrada", essencial para o passo 1.5 do `prompt-retomada.md` funcionar entre sessões.
- `checklist-fases.md`: cada fase ganha um item de existência física verificada por leitura direta; nova seção final "Gate de Existência Física — aplicável a toda fase".

### Adicionado: `agentes/00-onboarding-legado.md` (fork)

- A tag [INFERIDO] do original passa a ser resolvida como Tier 2 (com fonte observada no código) ou ADR nova, populando `decisoes-autonomas.md` já na reconstrução retroativa — um sistema legado entrando no fork começa com o mesmo padrão de rastreabilidade de um projeto novo.
- A tag [PENDENTE DE CONFIRMAÇÃO] continua sendo, por definição, Bloqueio Genuíno — nunca resolvida sozinha, mesmo no modo mais autônomo.

### Adicionado: `GUIA-DE-INICIO-RAPIDO.md` (fork)

- Reescrito para explicar o mecanismo central deste fork: nada pausa por padrão, você controla os freios pela forma como fraseia o pedido inicial. Tabela de frases-padrão. Seção nova sobre como e quando usar o Agente 9 (Auditor Externo). Lista de erros comuns específicos deste fork (confundir "disse que criou" com "criou", auditar com a mesma sessão que desenvolveu, etc.).

### Fechado: Bloco A do `CRONOGRAMA.md`

- Todos os 20 itens do checklist de construção do fork estão concluídos, exceto as 3 decisões que dependem de confirmação do usuário (nome definitivo, repositório separado vs. pasta no mesmo repo, comportamento de Bloqueio Genuíno) — documentadas com default explícito no `README.md`.
- `CRONOGRAMA.md` reescrito: Bloco A vira histórico fechado; Bloco B (fluxo de uso) ganha referência ao Agente 9 nas frases-padrão e no fluxograma.

### Estado do fork nesta versão

Fork completo e utilizável de ponta a ponta: todos os arquivos equivalentes ao Esquadrão Dev original existem, mais o Agente 9 (Auditor Externo), exclusivo deste fork. Nenhum item pendente de geração — restam só as 3 confirmações do usuário sobre defaults assumidos.

## v1.1 — Correção: regra de idioma como regra de topo, independente de releitura de arquivo de agente

### Motivação

Uma verificação ad hoc de status de épico (build + testes + leitura de `entregas/*.md`), pedida no meio de uma sessão já em andamento, foi respondida inteiramente em inglês. Causa raiz: a instrução de idioma só existia no cabeçalho de cada arquivo de agente individualmente — em um pedido solto, sem releitura formal de nenhum arquivo de agente naquele turno, essa instrução nunca chegou a valer. O problema foi agravado pela saída de ferramentas (build/testes) estar naturalmente em inglês, o que a sessão espelhou também na própria narração/conclusão.

Mesmo padrão de causa raiz dos três achados que originaram a v0.1 deste fork: uma proteção condicionada a um gatilho específico (aqui, "ter relido o arquivo certo") não é uma proteção confiável quando o pedido foge do fluxo padrão.

### Corrigido: `orquestrador.md`

- Nova seção **"Regra de topo (idioma): vale para toda resposta desta sessão, com ou sem releitura de arquivo de agente"**, inserida logo após a Regra de Topo de pausa explícita, com o mesmo nível de prioridade. Idioma Português (Brasil) passa a valer para qualquer resposta do projeto — incluindo verificações ad hoc, auditorias soltas, retomadas de sessão — independente de qual arquivo foi lido por último. Saída bruta de ferramentas (build/terminal/logs) pode continuar em seu idioma original; a narração, análise e conclusão sobre essa saída, nunca.

### Corrigido: `agentes/09-auditor-externo.md`

- Reforço explícito logo no início do arquivo: a regra de idioma vale mesmo em auditoria parcial/ad hoc, mesmo que o pedido do humano seja informal e não repita a instrução — não depende do agente ter sido "instanciado" colando o arquivo inteiro do zero.

### Pendente para próximas entregas

- Nenhum item de arquivo pendente nesta correção — v1.0 permanece a entrega completa de todos os arquivos do fork. v1.1 é uma correção pontual de comportamento transversal, não uma nova geração de artefato.
- Recomenda-se, na próxima retomada de projeto real (`prompt-retomada.md`), verificar se alguma resposta anterior à v1.1 foi produzida em idioma incorreto por este mesmo motivo — não é necessário refazer o conteúdo técnico dessas respostas, só sinalizar a divergência de formato caso encontrada (mesmo tratamento já dado a outras divergências de formato no passo 2.5 do `prompt-retomada.md`).