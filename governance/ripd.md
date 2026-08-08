# Parecer de Proporcionalidade - protecao de dados

> **Tipo de julgamento:** Parecer de Proporcionalidade (nao RIPD completo).
> **Por que:** o sistema nao trata dados de titulares. O tratamento possivel e **incidental e
> efemero**, restrito a conteudo transitivo colado pelo proprio operador e a evidencia de
> auditoria. Art. 38 da LGPD exige RIPD quando ha tratamento que possa gerar risco as
> liberdades civis e aos direitos fundamentais dos titulares; aqui o registro proporcional
> e este parecer. O tipo exigido **nao e escolha**: `ci/audit_lgpd.py` o deriva de
> `governance/data-inventory.yaml` e reprova se o registrado nao corresponder.
>
> Produzido pela skill `/revisao-lgpd` (agente `harness/agents/privacy/`), na lente ING-06 da
> ingestao do alvo (CP-002). O registro tipado - fingerprint, issues, escopo nao avaliado -
> esta em `governance/privacy-review.yaml`; este arquivo e a prosa.

## 1. Papel do sistema

Derivado de governanca de um alvo: a **cadeia multagente de adequacao a LGPD**
(`danzeroum/squadPosLgpd`): a Mesa de Orquestracao A2A (arquivo unico HTML/JS que roda no
navegador do operador, sem servidor), o orquestrador Python (`src/orquestrador_a2a.py`) e a
harness de governanca deste repositorio (fiscais, WebQA Suite como padrao externo, registro
de riscos).

A proposta de valor **nao exige tratar dado pessoal**: o negocio e documentacao de
adequacao (envelopes entre agentes, documentos de privacidade, artefatos `CHK-*`) - nao
cadastro de pessoas naturais. O sistema nao coleta titular, nao mantem banco de dados, nao
expoe endpoint publico (`classification.internet_exposed: false`).

**Papel LGPD:** nenhum (`controller.role: none`). Nao e controlador nem operador de dados de
titulares. Dado de pessoa natural aparece somente como **conteudo transitivo**: o texto de
documentacao de privacidade que o operador cola no Painel da Mesa (pode conter PII de
terceiros no corpo daquele texto), e como identificadores de colaborador do proprio projeto.

**Escopo desta revisao:** todo o repositorio - metadados de negocio, arquitetura, design,
governanca, o que a colheita ING-02 registrou do alvo, e a configuracoes de CI. O que nao
foi avaliado esta listado em `privacy-review.yaml:not_assessed`.

## 2. Dados incidentais capturados

| Vetor | Dado possivel | Natureza |
|---|---|---|
| Documentacao de privacidade colada no Painel | PII de terceiros eventualmente presente no texto livre (que transita para a API da orquestradora, incluindo provedor externo) | incidental, transitivo (RAM + localStorage) |
| Chave e token da API da orquestradora (`localStorage`) | credencial de integracao - **nao e dado pessoal**; a exportacao JSON e declarada no alvo como saindo **sem** eles | segredo do operador |
| Configuracao do ciclo (links dos 5 chats, modelo, base-URL) | configuracoes, sem pessoa | configuracao |
| `harness/runs/` | corpo de resposta do alvo auditado em modo `passive` - eventual dado pessoal do sistema auditado | incidental, efemero |
| Artifacts do CI (`harness/reports/`) | laudos derivados da evidencia acima | incidental, efemero |
| `project.yaml:business.stakeholders` | identificacao dos responsaveis pelo projeto (handles de conta) | dado pessoal de colaborador |
| Metadados de commit | nome e e-mail do autor | inerente ao Git, fora do controle da aplicacao |
| **Artifact e log do CI em repositorio publico** | os laudos acima, baixaveis por qualquer usuario | incidental, efemero, **publico** |

Nenhum desses e dado sensivel (Art. 5, II). Nenhum e coletado de titular-cliente. A varredura
deterministica de `ci/audit_lgpd.py` sobre a superficie declarada em `harness/stages.yaml`
retorna zero identificadores com forma de dado pessoal fora do inventario.

## 3. Controles proporcionais

Aplicados na hierarquia **nao coletar > mascarar na escrita > reter pouco > criptografar** -
criptografia e segunda linha para dado ja minimizado, nao a primeira resposta.

1. **Nao coletar (primeira linha).** A cadeia nao cria cadastro nem coleta de titular; o
   unico texto que existe e o que o operador cola deliberadamente, para o proprio ciclo de
   adequacao. Nao ha coleta a minimizar alem disso.
2. **Minimizar segredo.** Chave e token ficam apenas em `localStorage` no navegador do
   operador, e o JSON de exportacao sai sem eles - minimizacao declarada no alvo. A janela
   restante (segredo no cliente, superficie XSS/device) e registrada em `RISK-ACCESS-001`
   com niveis em `pending_judgment`: a lente de ingestao nao julga; ING-07 promove.
3. **Nao versionar - com a excecao declarada.** `workspace/` e area de trabalho efemera do
   processo de adocao; `harness/runs/`, `harness/reports/` e `harness/state/` sao
   gitignored: a evidencia bruta nao entra no history do Git, de onde nao se apaga. A unica
   excecao e `harness/state/ledger.jsonl`, versionado a partir do CP-026: o schema (`additionalProperties: false`)
   so admite hashes, SHAs, IDs opacos, enums, timestamps e refs canonicas - nao existe campo
   onde nome, e-mail, login ou texto caibam. A criacao humana, quando indispensavel, usa
   `actor_ref` pseudonimizado (`^anon:[0-9a-f]{16}$`), com a tabela de reidentificacao fora
   deste repositorio.
4. **Reter pouco.** `evidence_retention_days: 90` em `project.yaml`, `retention_days: 90` em
   `tests/qa/campanha.yaml` e `retention-days: 90` nos dois uploads de artifact - a
   igualdade entre os tres e fiscalizada (`check_evidence_retention`). Divergir e mentira
   de retencao.
5. **Sanitizacao mora fora.** Os achados chegam sanitizados pela WebQA Suite
   (`harness/schemas/report.schema.json`); este projeto nao pode afrouxar regra que nao possui
   (consequencia do ADR-001) e registra essa dependencia como vetor de risco conhecido.
6. **Registro das operacoes sempre em dia.** `governance/data-inventory.yaml` e fiscalizado
   a cada push: a varredura de tratamento-sombra cobre todas as superficies declaradas em
   `harness/stages.yaml`, incluindo os metadados novos da ingestao (capacidades,
   componentes, interfaces, superficies de UI). Se o alvo passou a tratar campo com forma
   de dado pessoal, o CI reprova - nao inventa isencao.
7. **Encarregado (Art. 41):** nao indicado, dispensado enquanto `controller.role` for
   `none` - e o parecer registra que o primeiro campo no inventario muda o tipo de
   julgamento para RIPD completo, passa a exigir encarregado e os endpoints do Art. 18
   (tres travas disparam juntas).

## 4. Controles descartados, com justificativa

- **Criptografia por campo / KMS** - desproporcional: nao ha banco de dados; a evidencia e
  efemera (90 dias) e sanitizada pelo padrao externo; o unico segredo vive em `localStorage`
  do navegador do operador, fora do alcance de KMS de repositorio. Reavaliar se o inventario
  deixar de ser vazio.
- **Endpoints de direitos do titular (Art. 18)** - nao aplicado: nao ha titular. O schema
  permite `null` nos quatro direitos **enquanto** `fields` estiver vazio e passa a cobra-los
  no primeiro campo inventariado.
- **RIPD completo (8 secoes)** - desproporcional hoje, e o proprio fiscal recusaria:
  `controller.role: none` exige este parecer. Vira obrigatorio automaticamente na mudanca
  do papel.
- **Plano formal de resposta a incidente (Art. 48)** - desproporcional para `role: none`:
  nao ha base de titulares a notificar. Cenarios considerados (runner de CI comprometido
  exfiltrando evidencia em job `passive`) seguem mitigados por retencao de 90 dias
  fiscalizada, por `harness/runs/` nunca virar artifact e pelos modos de rede serem
  `human_only` em job segregado.
- **Regime formal de transferencia internacional (Art. 33)** - o texto colado pode transitar
  pela API da orquestradora (provedor externo): fluxo incidental do operador, sem
  regularidade de tratamento, registrado em `RISK-PRIV-003` (`pending_judgment`). Gatilho
  de reavaliacao: o transito virar fluxo do produto.

## 5. Riscos residuais

| Risco | Severidade | Tratamento |
|---|---|---|
| Texto de doc colado com eventual PII transitando a provedor externo, sem clausulas formais (Art. 33) | `pending_judgment` - `RISK-PRIV-003`, julgado em ING-07 | Incidencia pontual e opcional do proprio operador; sem fluxo regular de titular. Sem o julgamento humano, nao ha fechamento. |
| Credencial da orquestradora em `localStorage` (superficie XSS/device) | `pending_judgment` - `RISK-ACCESS-001`, julgado em ING-07 | Minimizacao declarada pelo alvo (export sem chave/token); sem fiscal do lado deste repositorio. |
| Auditoria `passive` contra alvo de producao capturar PII em `harness/runs/` | Medio | Sanitizacao no padrao externo + retencao de 90 dias + evidencia nao versionada. Reabrir o parecer se o alvo de `tests/qa/config.yaml` deixar de ser ambiente de teste. |
| Laudo em artifact de repositorio publico, se a sanitizacao do padrao externo falhar | Baixo | `harness/runs/` nunca vira artifact; laudos citam identificadores, nao valores. |
| PII entrando sem inventariar | Medio | `RISK-PRIV-001`: varredura de tratamento-sombra a cada push. |
| Este parecer envelhecer em relacao ao sistema | Medio | `RISK-PRIV-002`: `scope_fingerprint` conferido a cada push. |

## 6. Aprovacao

- Encarregado (DPO): _nao indicado - dispensado enquanto `controller.role` for `none`
  (Art. 41)_
- Revisor de Engenharia: ______________________  Data: ____/____/________

> Este parecer e o registro tipado que cobre o estado identificado pelo `scope_fingerprint`.
> Mudou o escopo (primeiro campo no inventario, mudanca em `target.lock` ou
> `tests/qa/config.yaml`, campo com forma de PII fora do inventario), o parecer deixa de
> falar deste sistema e `ci/audit_lgpd.py` reprova ate que ele seja refeito.