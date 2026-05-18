# Desafio Prático — Frameworks de Prompt Engineering

Atividade prática da disciplina de IA Aplicada, com foco em engenharia de prompts estruturados para cenários reais de DevOps e SRE. Cada questão aplica um framework diferente para resolver um problema técnico concreto da empresa fictícia **Hill Valley Tech**.

---

## Contexto: Hill Valley Tech

A Hill Valley Tech é uma empresa de tecnologia com cinco sistemas em produção:

| Sistema | Papel |
|---|---|
| **Chronos** | API gateway — ponto de entrada de todo tráfego |
| **Ledger** | Data warehouse PostgreSQL com histórico de transações |
| **Reactor** | Processamento assíncrono via filas de mensagens |
| **Beacon** | Observabilidade: métricas, logs e alertas |
| **Lift** | Produto em beta em amadurecimento |

---

## Frameworks utilizados

| Framework | Componentes | Melhor aplicado em |
|---|---|---|
| **R-T-F** | Role · Task · Format | Tarefas técnicas com output bem definido |
| **T-A-G** | Task · Action · Goal | Análise de dados e queries determinísticas |
| **B-A-B** | Before · After · Bridge | Modernização e refatoração de artefatos existentes |
| **C-A-R-E** | Context · Action · Result · Example | Geração de código com padrão de estilo de referência |
| **R-I-S-E** | Role · Input · Steps · Expectation | Documentação operacional e análise de múltiplos artefatos |

---

## Questões

### Q1 — Dockerfile para o Lift `[R-T-F]`
Geração de um Dockerfile de produção para uma API Python/Flask migrando de VMs para Kubernetes. Cobre multi-stage build, usuário não-root, layer caching, HEALTHCHECK e CMD em exec form.

### Q2 — Script de backup do Ledger `[R-T-F]`
Criação de um script bash para backup automatizado do PostgreSQL em produção: `pg_dump | gzip`, upload para S3, retenção de 30 dias, logging estruturado e shell defensivo com `set -euo pipefail` e trap.

### Q3 — Relatório de redução de custos cloud `[T-A-G]`
Análise de um breakdown de custos AWS (12 serviços, ~USD 41.800/mês) para identificar oportunidades de economia priorizadas por impacto, com meta de 15% de redução sem degradar SLA.

### Q4 — Relatório mensal de transações do Ledger `[T-A-G]`
Escrita de uma query SQL para consolidar transações por mês e categoria nos últimos 6 meses, alimentando uma apresentação executiva. Dois modelos diferentes convergiram para a mesma query — evidência de especificação correta.

### Q5 — Modernizar deployment legado `[B-A-B]`
Modernização de um manifest Kubernetes de 3 anos: réplica única → HA, `:latest` → tag semântica, secrets em plain text → `secretKeyRef`, sem probes → liveness/readiness, sem securityContext → rootless.

### Q6 — Módulo Terraform no padrão interno `[C-A-R-E]`
Criação de um módulo Terraform reutilizável para buckets S3 seguindo o padrão de compliance da empresa: tags obrigatórias, prefixo `hvt-`, encryption, versioning, Block Public Access e logging.

### Q7 — Runbook para alerta recorrente `[R-I-S-E]`
Documentação operacional para o alerta `[CRITICAL] High memory usage on Chronos API pods (>85% for 10min)`, disparado ~4x por semana. O runbook cobre diagnóstico, mitigação, critérios objetivos de escalação e encerramento.

### Q8 — Postmortem técnico de incidente em produção `[R-I-S-E]`
Análise de um incidente em andamento durante pico de tráfego, com quatro artefatos reais (changelog de deploy, métricas, logs de pod, estado da fila). O postmortem suporta a decisão entre rollback e scaling emergencial em 20 minutos. Esta questão inclui comparação explícita com outros frameworks candidatos (B-A-B e T-A-G).

---

## Estrutura de cada questão

```
Questão XX - Nome/
├── prompt_base.txt      # Prompt estruturado com o framework aplicado
├── output_sonnet4.6.txt # Output gerado pelo Claude Sonnet 4.6
├── output_gemini3.txt   # Output gerado pelo Gemini 3
└── Justificativa.txt    # Análise de como os componentes do framework
                         # aparecem no prompt e comparação entre outputs
```

---

## Modelos utilizados

- **Claude Sonnet 4.6** (Anthropic)
- **Gemini 3** (Google)

Os dois modelos foram usados em paralelo em todas as questões para comparar como prompts bem estruturados produzem outputs convergentes (ou onde divergem e por quê).
