<!-- GENERATED: não editar; rodar ci/alignment_report.py -->
<!-- O --check do CI contradiz qualquer edição manual: edita-se a FONTE, não o derivado. -->
# Alinhamento entre departamentos

Matriz derivada do metadado declarado. Ela responde a pergunta que os demais fiscais não
fazem: **o que ficou de fora?**

## Cobertura de risco por capacidade

| Capacidade | risk_level | Riscos que a cobrem |
|---|---|---|
| `CAP-CUSTO` | low | — |
| `CAP-DEMO` | low | — |
| `CAP-ESTADO` | medium | `RISK-PRIV-003` |
| `CAP-MESA` | high | `RISK-ACCESS-001`, `RISK-PRIV-003` |
| `CAP-ORCH` | high | `RISK-PRIV-003` |
| `CAP-PREFLIGHT` | medium | — |
| `CAP-SONDA` | medium | — |

## Componentes

| Componente | Status | Capacidade | Implementa | Coberto por risco |
|---|---|---|---|---|
| `CMP-AGENTE-API` | proposed | `CAP-ORCH` | — | sim |
| `CMP-CORE` | proposed | `CAP-ORCH` | — | não |
| `CMP-CUSTO` | proposed | `CAP-CUSTO` | — | não |
| `CMP-DEMO` | proposed | `CAP-DEMO` | — | não |
| `CMP-MESA` | proposed | `CAP-MESA` | — | não |
| `CMP-ORQ-PY` | proposed | `CAP-ORCH` | — | não |
| `CMP-ORQUESTRADORA` | proposed | `CAP-ORCH` | — | não |
| `CMP-PILOTO` | proposed | `CAP-ORCH` | — | não |
| `CMP-PREFLIGHT` | proposed | `CAP-PREFLIGHT` | — | não |
| `CMP-PROMPTS` | proposed | `CAP-ORCH` | — | não |
| `CMP-PROTOCOL` | proposed | `CAP-ORCH` | — | não |
| `CMP-PROVEDORES` | proposed | `CAP-ORCH` | — | sim |
| `CMP-SONDA` | proposed | `CAP-SONDA` | — | não |
| `CMP-VOO` | proposed | `CAP-ORCH` | — | não |

## Riscos por área

| Área | Total | Abertos |
|---|---|---|
| access | 4 | 2 |
| data | 3 | 1 |
| dependencies | 1 | 0 |
| governance | 15 | 2 |
| webqa | 1 | 0 |

## Pendências de alinhamento

Nenhuma. Todo ativo relevante está coberto ou tem isenção declarada.
