# Prompt de Retomada de Projeto — Modo Autônomo — cole no início de qualquer chat/IA nova

> Idioma: responda sempre em Português (Brasil) em qualquer situação, inclusive em texto de raciocínio/narração intermediária.

> Fork do `prompt-retomada.md` do Esquadrão Dev original. Este é o ponto de entrada único ("bootstrap") de qualquer sessão nova neste projeto. Cole este prompt inteiro antes de pedir qualquer coisa — ele força a leitura do estado real (não só do que foi narrado em conversas anteriores) antes de qualquer ação. Seções marcadas **[NOVO — MODO AUTÔNOMO]** substituem/complementam o comportamento do original.

> **v1.2 — Correção: limite de escopo da retomada.** Duas sessões reais rodaram este mesmo prompt sobre o mesmo projeto: uma diagnosticou e parou em ~6 minutos; a outra, sem nenhuma instrução diferente, passou 30+ minutos gerando uma migration de banco nova e editando arquivos de teste até fazê-los passar. Causa raiz: o passo 2.4 pede "rode build+testes reais" para *confirmar* estado, mas não proíbe *corrigir* o que a verificação encontrar quebrado — e sem esse limite, debugar até passar é o comportamento mais natural para uma sessão com acesso a terminal. Seções marcadas **[AJUSTADO v1.2]** corrigem isso.

> **v1.3 — Correção: profundidade de diagnóstico e persistência de achados.** Uma auditoria externa sobre a v1.2 identificou dois furos residuais: (1) o limite de escopo da v1.2 restringe *ação* de correção, mas não restringe *profundidade de investigação* — nada impedia uma sessão de gastar o mesmo tempo "só diagnosticando" cada falha em detalhe sem nunca editar um arquivo; (2) um achado registrado no campo `TRABALHO DE CORREÇÃO NECESSÁRIO` do Formato de Diagnóstico não tinha destino formal — se a sessão parasse ali, o achado só existia no histórico daquele chat, não sobrevivia para uma sessão/IA futura. Seções marcadas **[AJUSTADO v1.3]** corrigem isso.

## 0. Verifique se este é um sistema legado sem artefatos do framework

(Idêntico ao original.) Existe código real deste sistema, mas não existe `estado-projeto.md` populado? Se sim, PARE — direcione para `agentes/00-onboarding-legado.md` antes de continuar.

## 1. Leia os arquivos de definição dos agentes

Leia todos os arquivos de `agentes/` (00 a 09, incluindo o novo Agente 9 — Auditor Externo, só relevante se o usuário pedir auditoria) e o `orquestrador.md` deste fork, para entender papel, formato de entrada/saída, critério de "pronto" de cada fase, e — diferente do original — as regras de modo autônomo (Gate de Existência Física, regra de pausa explícita, decisões documentadas em `decisoes-autonomas.md`).

## [NOVO — MODO AUTÔNOMO] 1.5. Verifique se há uma pausa em aberto que ainda não foi resolvida

Antes de ler qualquer artefato de conteúdo, confira o Formato de Status mais recente registrado na sessão anterior (se disponível) ou pergunte ao usuário: **havia uma instrução de pausa ativa quando a sessão anterior encerrou** (ex: "gere a documentação e aguarde autorização")? Se sim, e o usuário não deu ainda a autorização/ajuste correspondente nesta nova sessão, **não prossiga automaticamente** — reapresente o ponto em que parou e aguarde a decisão dele, exatamente como faria se a sessão nunca tivesse sido interrompida. Retomar uma sessão não é, por si só, uma autorização para prosseguir além de uma pausa que o usuário pediu.

## 2. Leia o estado real do projeto

(Idêntico ao original — `estado-projeto.md` e todos os artefatos já gerados na pasta do projeto, incluindo módulos se 4+, `contratos/`, `planos/tarefa-[ID].md`, `entregas/tarefa-[ID].md`.)

**[NOVO — MODO AUTÔNOMO]** Leia também `decisoes-autonomas.md` na íntegra (ou pelo menos os blocos de fechamento de épico mais recentes) — ele é, neste fork, tão essencial quanto `estado-projeto.md` para entender o que já foi decidido e por quê. Preste atenção especial à seção "Bloqueios Genuínos" desse arquivo: qualquer item lá sem resolução é equivalente, em gravidade, a uma "Dívida Técnica" não resolvida do `estado-projeto.md`.

**Regra de citação de IDs**: (idêntico ao original) nunca cite um ID de pendência ou decisão isolado — inclua sempre o texto correspondente na mesma linha, seja de `estado-projeto.md` ou de `decisoes-autonomas.md`.

## [NOVO — MODO AUTÔNOMO] 2.4. Verifique a existência física real de tudo que o estado alega — nunca confie na narração

Este passo não existe no `prompt-retomada.md` original porque lá o humano acompanhava tudo em tempo real. Neste fork, é obrigatório: para cada artefato que `estado-projeto.md` ou o último Formato de Status registrado alegam como "Concluído" ou "existente", **confirme por leitura direta do arquivo** (não pela narração de uma resposta anterior, mesmo que pareça confiável). Se encontrar qualquer divergência entre o que foi alegado e o que existe de fato:

1. Não prossiga como se nada tivesse acontecido.
2. Registre o incidente explicitamente (o que foi alegado, o que foi encontrado de verdade).
3. Reconstrua o artefato ausente a partir do histórico de conversa disponível, marcando-o como reconstrução retroativa — nunca como levantamento original.
4. Revalide se as decisões já tomadas nas fases seguintes ainda se sustentam contra o artefato reconstruído.
5. Informe isso ao usuário antes de continuar qualquer outra tarefa (mesma disciplina da seção "Disciplina de escrita em arquivos de estado" do `orquestrador.md`, aplicada aqui à retomada).

Isso é o mesmo Gate de Existência Física do `orquestrador.md` deste fork, aplicado especificamente ao momento de retomada — que é justamente quando esse tipo de furo tende a ser descoberto (uma sessão nova, sem o contexto "eu tenho certeza que criei isso" da sessão anterior, é o momento mais propício para pegar a discrepância).

**[AJUSTADO v1.2] Limite de escopo: verificação física não é execução de correção.** Rodar build e a suíte de testes **uma vez** para confirmar o estado real (compila? os testes que deveriam passar passam?) faz parte deste passo. O que **não faz parte deste passo**, mesmo que pareça economia natural de esforço ("já que estou vendo o erro, já corrijo"):

- Gerar migrations de banco novas, aplicar `database update`, ou qualquer alteração de schema.
- Editar código de produção ou de teste para fazer algo que estava falhando passar a passar.
- Rodar retry loops de diagnóstico (reproduzir, hipotetizar, corrigir, rodar de novo) até a suíte fechar verde.
- Qualquer ação que, no framework, pertence ao Agente 5 (Desenvolvedor) ou ao Agente 6 (QA) — mesmo que você, nesta sessão, tecnicamente consiga assumir esses papéis.

Se a verificação revelar build quebrado, migration pendente, ou testes falhando: **isso é um achado do diagnóstico, não um convite para corrigir agora.** Registre exatamente o que foi encontrado (comando + saída real) no campo `TRABALHO DE CORREÇÃO NECESSÁRIO` do Formato de Diagnóstico (passo 4) e pare ali — a decisão de seguir para correção, e qual agente assume isso, acontece depois do diagnóstico ser reportado, nunca durante ele. Se você decidir (ou o usuário autorizar) seguir para a correção na sequência desta mesma sessão, faça isso assumindo formalmente o Agente 5 ou 6 correspondente — plano/self-check ou relatório de QA, evidência real, e reabertura do ciclo Dev→QA→Revisão se algo for alterado — nunca como edição solta ainda dentro do papel de "sessão de retomada".

**[AJUSTADO v1.3] O limite de escopo vale também para profundidade de investigação, não só para ação de correção.** Registrar comando + saída da falha (ex: nome do teste, mensagem de erro, stack trace relevante) já é suficiente para este passo. Não é necessário, aqui, abrir cada arquivo de teste que falhou, ler o código de produção correspondente, formular hipótese de causa raiz, ou comparar contra a especificação técnica para entender "por que" — isso é trabalho de diagnóstico que pertence ao Agente 5 (Diagnóstico Disciplinado de Bugs) ao assumir formalmente a correção, não à retomada. Gastar tempo investigando sem editar nenhum arquivo ainda viola o espírito deste limite, mesmo que a letra ("não corrigi nada") esteja tecnicamente respeitada.

**[AJUSTADO v1.3] Se a própria verificação exigir repetição, isso já é achado, não esforço legítimo a insistir.** Uma segunda tentativa de build/teste é aceitável quando a causa é puramente operacional e óbvia (ex: processo de teste anterior ainda travando a porta/arquivo, exigindo encerrar e rodar de novo uma vez). Mas se confirmar o estado exigir múltiplas rodadas por incerteza sobre o resultado (build instável, teste piscando entre passar/falhar, ambiente inconsistente), **isso já é, em si, o achado a registrar** — não continue tentando até obter uma leitura "limpa". Descreva a instabilidade encontrada no campo `TRABALHO DE CORREÇÃO NECESSÁRIO` e pare.

## 2.5. Verifique se os artefatos existentes estão no formato da versão atual dos agentes

(Idêntico ao original — comparar contra `agentes/` e `templates/` da versão atual, sinalizar divergência de formato sem reescrever sozinho.)

**[NOVO]** Verifique também: o projeto tem `decisoes-autonomas.md`? Se o projeto foi iniciado antes desta versão do fork existir (ou começou no Esquadrão Dev original e está migrando para este fork), esse arquivo pode não existir ainda — não é erro, é ausência de versão anterior. Pergunte ao usuário se ele quer que você reconstrua retroativamente as decisões já tomadas (a partir de `pendencias-revisao.md`, se existir, ou do histórico de conversa) antes de prosseguir com decisões novas.

## 2.6. Verifique se há uma tarefa travada no meio

(Idêntico ao original — comparar status registrado contra artefatos reais: plano existe? entrega existe? código existe?)

**[NOVO]** Adicione a esta verificação: se a tarefa travada tinha um plano, ele tem a linha `Status deste plano: Plano autoaprovado em [data], checklist 3/3`? Se o plano existe mas não tem essa linha, isso é sinal de que o self-check (Agente 5 deste fork) nunca foi de fato aplicado — trate como equivalente a "plano não aprovado" no framework original, mesmo que pareça que a implementação já começou.

## 2.7. Ao verificar se uma decisão/pergunta já está definida nos artefatos (auditoria retroativa)

**[NOVO — MODO AUTÔNOMO — ordem de precedência ajustada]** A ordem de precedência do original ganha uma camada nova, inserida entre o plano da tarefa e o contrato:

1. `planos/tarefa-[ID].md` da tarefa relevante — tabela de Classificação da Decisão e "Resolvida?".
2. **`decisoes-autonomas.md`** — se a decisão foi resolvida como Tier 2 ou ADR nova pelo fluxo autônomo, a entrada lá é a fonte de maior autoridade depois do plano específico, porque é mais recente e mais explícita que a especificação técnica ou o contrato. **[camada nova deste fork]**
3. `contratos/modulo-[nome].md`.
4. `especificacao-tecnica.md` (arquivo-mãe e/ou módulo).
5. `documento-requisitos.md` (incluindo a seção 7 com restrições travadas explicitamente pelo usuário na Fase 1 — essa tem precedência sobre qualquer decisão autônoma que a contrarie, se existir conflito).

Nunca conclua "já resolvido" ou "ainda em aberto" com base só nos níveis 3-5 sem checar antes os níveis 1-2. O **sinal de alerta obrigatório** do original (duas verificações chegando a conclusões opostas = evidência de checagem incompleta) continua valendo integralmente, agora incluindo `decisoes-autonomas.md` como possível causa da divergência — ex: uma verificação pode ter lido a Especificação Técnica genérica sem checar se aquela decisão específica já foi refinada/sobrescrita por uma entrada posterior em `decisoes-autonomas.md`.

## 3. Diagnostique em qual fase o projeto realmente está

(Idêntico ao original — comparar contra `templates/checklist-fases.md`, aplicar Gate de Cobertura antes de aceitar "pronto para entrega final".)

**[NOVO]** Ao aplicar o Gate de Cobertura, verifique também se alguma tarefa foi marcada "Concluída" só com base em alegação sem evidência (ver Camada 4 do Agente 9 — Auditor Externo, se você quiser aplicar esse nível de rigor mesmo sem uma sessão de auditoria separada rodando).

## 4. Reporte o diagnóstico antes de agir

Mesmo formato do original, com dois campos novos:

```
FASE ATUAL REAL: [nome da fase]
VERIFICAÇÃO FÍSICA REALIZADA: [confirme que você aplicou o passo 2.4 — liste os artefatos checados por leitura direta, não apenas os alegados]
PAUSA EM ABERTO (se houver, do passo 1.5): [qual era a instrução de pausa e se ela ainda está ativa]
TAREFA TRAVADA NO MEIO (se houver): [ID + status registrado + o que os artefatos reais mostram + o que falta decidir]
FASES CONCLUÍDAS E VALIDADAS: [lista]
FASES INICIADAS MAS INCOMPLETAS: [lista, com o que falta especificamente]
GATE DE COBERTURA RF/RNF (se todos os épicos concluídos): [checagem completa]
COMPATIBILIDADE DE FORMATO COM A VERSÃO ATUAL: [divergências do passo 2.5, incluindo ausência de decisoes-autonomas.md se aplicável]
DÍVIDA TÉCNICA NÃO RESOLVIDA: [lista]
BLOQUEIOS GENUÍNOS EM ABERTO (de decisoes-autonomas.md): [lista, se houver]
INCONSISTÊNCIAS ENCONTRADAS ENTRE ARTEFATOS: [lista, se houver]
TRABALHO DE CORREÇÃO NECESSÁRIO (fora do escopo desta retomada) [NOVO — v1.2]: [tudo que a verificação do passo 2.4 encontrou quebrado/pendente mas não foi corrigido aqui — ex: "migration pendente, nunca aplicada ao banco de testes"; "3 de 87 testes falhando: TransferenciasTests.Transferencia_CancelarAntesDeEnviar_Ok, ..."; comando + saída real de cada um. Se nada foi encontrado quebrado, escreva "Nenhum — build e testes rodados uma vez, sem falhas"]
PRÓXIMO AGENTE A ATUAR: [nome do agente] — [motivo — se o motivo for corrigir algo listado no campo acima, diga isso explicitamente, ex: "Agente 5 — Desenvolvedor, para investigar e corrigir os 3 testes falhando listados acima, seguindo diagnóstico disciplinado de bugs"]
```

**Só prossiga automaticamente para o próximo passo se não houver pausa em aberto (campo acima).** Se houver, pare aqui e aguarde a decisão do usuário — mesma regra de topo do `orquestrador.md`.

**[NOVO — v1.2]** Isso vale com força extra quando `TRABALHO DE CORREÇÃO NECESSÁRIO` não estiver vazio: mesmo sem pausa em aberto, reportar o diagnóstico completo (incluindo esse campo) é sempre o próximo passo — nunca comece a corrigir no meio da própria verificação, mesmo que o fluxo esteja em modo autônomo sem pausa pedida. "Sem pausa em aberto" autoriza o Orquestrador a *decidir* qual agente assume a correção e seguir sem esperar aprovação humana; não autoriza pular a etapa de decidir isso formalmente e ir direto editando arquivos ainda dentro do papel de retomada.

**[AJUSTADO v1.3] Todo achado do campo `TRABALHO DE CORREÇÃO NECESSÁRIO` que não for corrigido nesta mesma sessão precisa ser promovido para a tabela de Dívida Técnica do `estado-projeto.md`, com ID sequencial Pxx**, antes de a sessão encerrar — mesmo que o achado pareça óbvio ou "com certeza vai ser corrigido logo em seguida". O relatório de diagnóstico desta retomada vive só no histórico deste chat; se uma sessão futura (ou outra IA) retomar o projeto sem ter acesso a este histórico, o único lugar confiável para encontrar esse achado é `estado-projeto.md`. Registrar só no Formato de Diagnóstico e nunca promover para lá é o mesmo tipo de furo que a Camada 1 do Agente 9 (Auditor Externo) já existe para pegar — "alegado mas não encontrado" — só que aqui é "achado mas não registrado de forma persistente".

## 5. Regras ao assumir o trabalho

(Idêntico ao original: não invente requisitos/decisões/tarefas não documentadas; não corrija inconsistência silenciosamente; assuma o papel do agente correspondente lendo o arquivo dele; siga "Execução Real" dos agentes 4/5/6 se houver terminal.)

**[NOVO]** Adicione: toda decisão que você tomar a partir daqui, se não estiver puramente conversando com o usuário na Fase 1, deve seguir o mesmo padrão de documentação em `decisoes-autonomas.md` do resto do fork — retomar uma sessão não é uma exceção que dispensa esse registro.

**[NOVO — v1.2]** Adicione também: se o diagnóstico do passo 4 apontou `TRABALHO DE CORREÇÃO NECESSÁRIO` e a sessão vai seguir para resolver isso, a transição para o papel do agente correspondente (5 ou 6) precisa ser explícita e completa — leia o arquivo daquele agente e assuma a disciplina dele por inteiro (self-check formal antes de codificar, evidência real com comando+saída, reabertura do ciclo QA→Revisor se algo já aprovado for alterado), exatamente como faria se estivesse chegando a essa tarefa pelo fluxo normal, nunca por já pertencer a esta mesma resposta de retomada. Um bug corrigido "de passagem" durante a verificação, sem plano/self-check e sem passar de novo por QA depois, é uma correção sem rede de segurança — o mesmo problema que a regra dura do Agente 6/7 já existe para evitar, aplicado aqui à própria sessão de retomada.