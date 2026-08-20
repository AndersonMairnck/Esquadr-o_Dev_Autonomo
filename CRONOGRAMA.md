# Cronograma de Uso — Esquadrão Dev Autônomo

> Este arquivo tem dois blocos: **Bloco A** (fechado nesta versão) é o histórico de construção do fork. **Bloco B** é o cronograma de uso do fork já pronto, num projeto real — este é o que você consulta no dia a dia.

---

## Bloco A — Construção do fork (concluído — v1.0)

| # | Item | Status |
|---|------|--------|
| 1 | `orquestrador.md` | ✅ |
| 2 | `agentes/01-analista-requisitos.md` | ✅ |
| 3 | `templates/decisoes-autonomas.md` | ✅ |
| 4 | `README.md` | ✅ |
| 5 | `CHANGELOG.md` | ✅ |
| 6 | `agentes/02-arquiteto-software.md` | ✅ |
| 7 | `agentes/03-designer-ux-ui.md` | ✅ |
| 8 | `agentes/04-planejador-tarefas.md` | ✅ |
| 9 | `agentes/05-desenvolvedor.md` | ✅ |
| 10 | `agentes/06-qa-testes.md` (cópia intencional) | ✅ |
| 11 | `agentes/07-revisor-seguranca.md` (cópia intencional) | ✅ |
| 12 | `agentes/08-documentador.md` (cópia intencional) | ✅ |
| 13 | `agentes/09-auditor-externo.md` (novo) | ✅ |
| 14 | `agentes/00-onboarding-legado.md` | ✅ |
| 15 | `prompt-retomada.md` | ✅ |
| 16 | `templates/estado-projeto.md` | ✅ |
| 17 | `templates/checklist-fases.md` | ✅ |
| 18 | `templates/plano-tarefa.md` | ✅ |
| 19 | `GUIA-DE-INICIO-RAPIDO.md` | ✅ |
| 20 | 3 decisões suas em aberto | ⬜ Ver `README.md` |

Todos os arquivos do framework têm equivalente neste fork. Único pendente real são as 3 confirmações suas (nome, local do repo, comportamento de Bloqueio Genuíno) — ver `README.md`.

---

## Bloco B — Fluxo real de uso, projeto por projeto

Ordem fixa, sem pular etapa, para não perder nada nem deixar artefato para trás.

```
┌─────────────────────────────────────────────────────────────────┐
│ 1. VOCÊ INICIA                                                    │
│    "Inicie o fluxo [+ instrução de até onde ir, ver B.1]"        │
└───────────────────────────┬─────────────────────────────────────┘
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│ 2. FASE 1 — REQUISITOS (Agente 1)                                 │
│    ÚNICA fase com conversa humana real.                          │
│    Doc externo? Ele lê, aplica checklist, sintetiza, SALVA         │
│    documento-requisitos.md (nunca usa o externo como final).      │
│    Pergunta final: "algo para travar como não-negociável?"        │
│    ✋ Só para aqui se você pedir "aguarde" explicitamente.         │
└───────────────────────────┬─────────────────────────────────────┘
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│ 3. FASE 2 — ARQUITETURA (Agente 2, autônomo)                      │
│    Decide stack/plataforma/pastas, documenta em                   │
│    decisoes-autonomas.md. Gate: especificacao-tecnica.md tem      │
│    que existir FISICAMENTE, verificado, antes de avançar.         │
└───────────────────────────┬─────────────────────────────────────┘
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│ 4. FASE 3 — DESIGN UX/UI (Agente 3, autônomo)                     │
│    Decide direção visual por inferência do público, documenta.    │
│    Gate: design-ux-ui.md tem que existir no disco.                │
└───────────────────────────┬─────────────────────────────────────┘
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│ 5. FASE 4 — PLANEJAMENTO (Agente 4, autônomo)                     │
│    Backlog completo, HITL antigo vira AFK Tier 2 documentado       │
│    (ou ADR nova). Gate: backlog.md tem que existir no disco.      │
│                                                                     │
│    ⬅── PONTO DE PAUSA TÍPICO ("gere a documentação e aguarde")    │
└───────────────────────────┬─────────────────────────────────────┘
                             ▼
            ┌────────────────┴────────────────┐
            ▼                                  ▼
   ┌──────────────────┐            ┌────────────────────────┐
   │ 6a. VOCÊ PEDE      │            │ 6b. VOCÊ AUTORIZA        │
   │ AJUSTE             │            │ "desenvolva o Épico 1    │
   │ Volta ao agente     │            │ todo e pare quando        │
   │ certo, corrige,     │            │ tiver tudo pronto"        │
   │ CONTINUA aguardando │            │                            │
   └──────────────────┘            │ 7. LOOP Dev→QA→Revisão     │
                                     │ por tarefa. Self-check     │
                                     │ (Teste do Júnior +          │
                                     │ Checklist 7/7 + decisões   │
                                     │ resolvidas) substitui        │
                                     │ aprovação humana do plano. │
                                     │                            │
                                     │ 8. CHECKPOINT DE ÉPICO      │
                                     │ (QA integração + coesão do │
                                     │ Revisor + fecha bloco em    │
                                     │ decisoes-autonomas.md)      │
                                     │                            │
                                     │ ✋ Para se você pediu        │
                                     │ "pare quando o épico        │
                                     │ estiver pronto"              │
                                     └──────────┬─────────────────┘
                                                ▼
                                     ┌────────────────────────┐
                                     │ 9. VOCÊ REVISA            │
                                     │ Lê decisoes-autonomas.md, │
                                     │ ou pede auditoria externa  │
                                     │ (Agente 9, sessão separada)│
                                     │                            │
                                     │ "prossiga Épico 2" ──────┼──▶ volta ao passo 7
                                     │ "ajuste X" ───────────────┼──▶ volta ao agente certo
                                     │ "siga até o fim sem       │
                                     │  mais pausas" ────────────┼──▶ roda até Documentação final
                                     └────────────────────────┘
```

### B.1 — Frases-padrão

| O que você quer | Frase |
|---|---|
| Só documentação, revisar tudo antes de código | "Inicie o fluxo, gere toda a documentação inicial (requisitos, arquitetura, design, backlog) e aguarde eu autorizar o desenvolvimento." |
| Documentação + 1 épico, depois revisar | "...e, depois de aprovado por mim, desenvolva o Épico 1 todo e pare quando tiver tudo pronto." |
| Rodar tudo sem pausa nenhuma | "Inicie o fluxo e construa o sistema completo, sem pausar entre fases — só me avise se cair em um bloqueio genuíno." |
| Retomar após ajuste, sem soltar de vez | "Ajuste [X] no [artefato] e volte a aguardar — não inicie o desenvolvimento ainda." |
| Liberar geral a partir de um ponto | "Pode seguir até o fim sem mais pausas, salvo bloqueio genuíno." |
| **[NOVO]** Auditoria de segunda opinião | Em sessão separada: "Leia `agentes/09-auditor-externo.md` e audite tudo que já foi produzido no projeto [X], com acesso só de leitura." |

### B.2 — Verificação de integridade a qualquer momento

> "Rode a verificação física de todos os artefatos até agora e me diga o que existe de fato no disco vs. o que o Formato de Status alega."

Isso força o Gate de Existência Física a rodar retroativamente sobre tudo já produzido na sessão.

### B.3 — Quando usar o Agente 9 (Auditor Externo)

Em qualquer pausa, antes de decidir "prossiga" ou "ajuste": abra uma sessão nova e separada (idealmente outro modelo), cole `agentes/09-auditor-externo.md`, dê acesso só de leitura, peça a auditoria. Você recebe um parecer com recomendação objetiva (prosseguir / prosseguir com ressalvas / recomendo pausar) sem IDs soltos nem jargão não traduzido. Use principalmente em marcos importantes: fim da documentação inicial, fim de épicos grandes, antes da entrega final.

---

## Status atual do seu projeto (preencha/atualize conforme avança)

| Campo | Valor |
|---|---|
| Nome do projeto | |
| Fase real do projeto (Bloco B) | |
| Última pausa pedida | |
| Última auditoria externa (Agente 9), se houve | |
| Próxima ação esperada de você | |
