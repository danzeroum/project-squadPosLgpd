<!-- GENERATED: não editar; rodar ci/generate_graph.py -->
# Mapa de relacionamento dos metadados

> Artefato DERIVADO dos metadados reais, não fonte de verdade. Editar aqui é trabalho
> perdido: o `--check` do CI contradiz a edição na hora mais cara.

Legenda: azul-escuro = projeto · azul = capacidade (`CAP-`) · ciano = componente (`CMP-`) ·
roxo = interface (`IFC-`) · verde = regra (`RULE-`) · rosa = superfície de UI (`UI-`) ·
amarelo = ADR · vermelho = risco (`RISK-`).

```mermaid
graph TD
  PROJ_project_squadposlgpd["project-squadposlgpd"]
  TEST_workspace_target_mesa_tests_aceite_test_mjs{{"aceite.test.mjs"}}
  TEST_workspace_target_mesa_tests_agente_api_test_mjs{{"agente-api.test.mjs"}}
  TEST_workspace_target_mesa_tests_config_test_mjs{{"config.test.mjs"}}
  TEST_workspace_target_mesa_tests_custo_test_mjs{{"custo.test.mjs"}}
  TEST_workspace_target_mesa_tests_degeneradas_test_mjs{{"degeneradas.test.mjs"}}
  TEST_workspace_target_mesa_tests_e2e_test_mjs{{"e2e.test.mjs"}}
  TEST_workspace_target_mesa_tests_engine_test_mjs{{"engine.test.mjs"}}
  TEST_workspace_target_mesa_tests_entrega_test_mjs{{"entrega.test.mjs"}}
  TEST_workspace_target_mesa_tests_espelho_guarda_test_mjs{{"espelho-guarda.test.mjs"}}
  TEST_workspace_target_mesa_tests_frescor_test_mjs{{"frescor.test.mjs"}}
  TEST_workspace_target_mesa_tests_orquestrador_py_test_mjs{{"orquestrador-py.test.mjs"}}
  TEST_workspace_target_mesa_tests_orquestradora_test_mjs{{"orquestradora.test.mjs"}}
  TEST_workspace_target_mesa_tests_piloto_tela_test_mjs{{"piloto-tela.test.mjs"}}
  TEST_workspace_target_mesa_tests_piloto_test_mjs{{"piloto.test.mjs"}}
  TEST_workspace_target_mesa_tests_preflight_test_mjs{{"preflight.test.mjs"}}
  TEST_workspace_target_mesa_tests_prompt_contrato_test_mjs{{"prompt-contrato.test.mjs"}}
  TEST_workspace_target_mesa_tests_prompts_agentes_test_mjs{{"prompts-agentes.test.mjs"}}
  TEST_workspace_target_mesa_tests_protocol_test_mjs{{"protocol.test.mjs"}}
  TEST_workspace_target_mesa_tests_real_deepseek_test_mjs{{"real-deepseek.test.mjs"}}
  TEST_workspace_target_mesa_tests_sonda_corpo_test_mjs{{"sonda-corpo.test.mjs"}}
  TEST_workspace_target_mesa_tests_telemetria_test_mjs{{"telemetria.test.mjs"}}
  TEST_workspace_target_mesa_tests_voo_demonstracao_test_mjs{{"voo-demonstracao.test.mjs"}}
  TEST_workspace_target_mesa_tests_voo_test_mjs{{"voo.test.mjs"}}
  TEST_workspace_target_src_orquestrador_a2a_py{{"orquestrador_a2a.py"}}
  TEST_workspace_target_tests_test_orquestrador_a2a_py{{"test_orquestrador_a2a.py"}}
  CAP_CUSTO["CAP-CUSTO<br/>Telemetria e orcamento de custo por uso de LLM"]
  PROJ_project_squadposlgpd -->|capacidade| CAP_CUSTO
  CAP_DEMO["CAP-DEMO<br/>Modo demonstracao da mesa"]
  PROJ_project_squadposlgpd -->|capacidade| CAP_DEMO
  CAP_ESTADO["CAP-ESTADO<br/>Estado persistente, exportacao/importacao e fila local (modo prancheta)"]
  PROJ_project_squadposlgpd -->|capacidade| CAP_ESTADO
  CAP_MESA["CAP-MESA<br/>Operacao da mesa: painel, transito, configuracao e linha do tempo"]
  PROJ_project_squadposlgpd -->|capacidade| CAP_MESA
  CAP_ORCH["CAP-ORCH<br/>Orquestracao A2A da cadeia de adequacao LGPD"]
  PROJ_project_squadposlgpd -->|capacidade| CAP_ORCH
  CAP_PREFLIGHT["CAP-PREFLIGHT<br/>Verificacao preflight e origem unica do modelo"]
  PROJ_project_squadposlgpd -->|capacidade| CAP_PREFLIGHT
  CAP_SONDA["CAP-SONDA<br/>Sonda de respostas brutas de agentes"]
  PROJ_project_squadposlgpd -->|capacidade| CAP_SONDA
  CMP_AGENTE_API["CMP-AGENTE-API<br/>agente-api.js"]
  CMP_AGENTE_API -->|realiza| CAP_ORCH
  CMP_AGENTE_API -->|depende| CMP_CORE
  CMP_AGENTE_API -->|depende| CMP_DEMO
  CMP_AGENTE_API -->|depende| CMP_ORQUESTRADORA
  CMP_AGENTE_API -->|depende| CMP_PILOTO
  CMP_AGENTE_API -->|depende| CMP_PROMPTS
  CMP_AGENTE_API -->|depende| CMP_PROTOCOL
  CMP_AGENTE_API -->|depende| CMP_PROVEDORES
  CMP_AGENTE_API -.->|testa| TEST_workspace_target_mesa_tests_agente_api_test_mjs
  CMP_CORE["CMP-CORE<br/>engine.js"]
  CMP_CORE -->|realiza| CAP_ORCH
  CMP_CORE -->|depende| CMP_PROTOCOL
  CMP_CORE -.->|testa| TEST_workspace_target_mesa_tests_engine_test_mjs
  CMP_CUSTO["CMP-CUSTO<br/>custo.mjs"]
  CMP_CUSTO -->|realiza| CAP_CUSTO
  CMP_CUSTO -->|depende| CMP_PROVEDORES
  CMP_CUSTO -.->|testa| TEST_workspace_target_mesa_tests_custo_test_mjs
  CMP_DEMO["CMP-DEMO<br/>demo.js"]
  CMP_DEMO -->|realiza| CAP_DEMO
  CMP_DEMO -->|depende| CMP_CORE
  CMP_DEMO -.->|testa| TEST_workspace_target_mesa_tests_aceite_test_mjs
  CMP_MESA["CMP-MESA<br/>Mesa-v1.html"]
  CMP_MESA -->|realiza| CAP_MESA
  CMP_MESA -->|depende| CMP_AGENTE_API
  CMP_MESA -->|depende| CMP_CORE
  CMP_MESA -->|depende| CMP_DEMO
  CMP_MESA -->|depende| CMP_ORQUESTRADORA
  CMP_MESA -->|depende| CMP_PILOTO
  CMP_MESA -->|depende| CMP_PROMPTS
  CMP_MESA -->|depende| CMP_PROTOCOL
  CMP_MESA -->|depende| CMP_PROVEDORES
  CMP_MESA -->|depende| CMP_VOO
  CMP_MESA -.->|testa| TEST_workspace_target_mesa_tests_e2e_test_mjs
  CMP_MESA -.->|testa| TEST_workspace_target_mesa_tests_telemetria_test_mjs
  CMP_MESA -.->|testa| TEST_workspace_target_mesa_tests_voo_demonstracao_test_mjs
  CMP_ORQ_PY["CMP-ORQ-PY<br/>orquestrador-py.test.mjs"]
  CMP_ORQ_PY -->|realiza| CAP_ORCH
  CMP_ORQ_PY -.->|testa| TEST_workspace_target_mesa_tests_orquestrador_py_test_mjs
  CMP_ORQ_PY -.->|testa| TEST_workspace_target_src_orquestrador_a2a_py
  CMP_ORQ_PY -.->|testa| TEST_workspace_target_tests_test_orquestrador_a2a_py
  CMP_ORQUESTRADORA["CMP-ORQUESTRADORA<br/>orquestradora.js"]
  CMP_ORQUESTRADORA -->|realiza| CAP_ORCH
  CMP_ORQUESTRADORA -->|depende| CMP_CORE
  CMP_ORQUESTRADORA -->|depende| CMP_CUSTO
  CMP_ORQUESTRADORA -->|depende| CMP_DEMO
  CMP_ORQUESTRADORA -->|depende| CMP_PROMPTS
  CMP_ORQUESTRADORA -->|depende| CMP_PROTOCOL
  CMP_ORQUESTRADORA -->|depende| CMP_PROVEDORES
  CMP_ORQUESTRADORA -->|depende| CMP_VOO
  CMP_ORQUESTRADORA -.->|testa| TEST_workspace_target_mesa_tests_orquestradora_test_mjs
  CMP_ORQUESTRADORA -.->|testa| TEST_workspace_target_mesa_tests_real_deepseek_test_mjs
  CMP_PILOTO["CMP-PILOTO<br/>piloto.js"]
  CMP_PILOTO -->|realiza| CAP_ORCH
  CMP_PILOTO -->|depende| CMP_AGENTE_API
  CMP_PILOTO -->|depende| CMP_CORE
  CMP_PILOTO -->|depende| CMP_DEMO
  CMP_PILOTO -->|depende| CMP_ORQUESTRADORA
  CMP_PILOTO -->|depende| CMP_PROTOCOL
  CMP_PILOTO -->|depende| CMP_PROVEDORES
  CMP_PILOTO -->|depende| CMP_VOO
  CMP_PILOTO -.->|testa| TEST_workspace_target_mesa_tests_degeneradas_test_mjs
  CMP_PILOTO -.->|testa| TEST_workspace_target_mesa_tests_piloto_tela_test_mjs
  CMP_PILOTO -.->|testa| TEST_workspace_target_mesa_tests_piloto_test_mjs
  CMP_PREFLIGHT["CMP-PREFLIGHT<br/>preflight.mjs"]
  CMP_PREFLIGHT -->|realiza| CAP_PREFLIGHT
  CMP_PREFLIGHT -->|depende| CMP_ORQUESTRADORA
  CMP_PREFLIGHT -->|depende| CMP_PROMPTS
  CMP_PREFLIGHT -->|depende| CMP_PROVEDORES
  CMP_PREFLIGHT -.->|testa| TEST_workspace_target_mesa_tests_preflight_test_mjs
  CMP_PROMPTS["CMP-PROMPTS<br/>prompt-orq.mjs"]
  CMP_PROMPTS -->|realiza| CAP_ORCH
  CMP_PROMPTS -->|depende| CMP_DEMO
  CMP_PROMPTS -->|depende| CMP_PILOTO
  CMP_PROMPTS -->|depende| CMP_PROTOCOL
  CMP_PROMPTS -->|depende| CMP_PROVEDORES
  CMP_PROMPTS -.->|testa| TEST_workspace_target_mesa_tests_prompt_contrato_test_mjs
  CMP_PROMPTS -.->|testa| TEST_workspace_target_mesa_tests_prompts_agentes_test_mjs
  CMP_PROTOCOL["CMP-PROTOCOL<br/>protocol.js"]
  CMP_PROTOCOL -->|realiza| CAP_ORCH
  CMP_PROTOCOL -.->|testa| TEST_workspace_target_mesa_tests_entrega_test_mjs
  CMP_PROTOCOL -.->|testa| TEST_workspace_target_mesa_tests_espelho_guarda_test_mjs
  CMP_PROTOCOL -.->|testa| TEST_workspace_target_mesa_tests_frescor_test_mjs
  CMP_PROTOCOL -.->|testa| TEST_workspace_target_mesa_tests_protocol_test_mjs
  CMP_PROVEDORES["CMP-PROVEDORES<br/>provedores.js"]
  CMP_PROVEDORES -->|realiza| CAP_ORCH
  CMP_PROVEDORES -->|depende| CMP_ORQUESTRADORA
  CMP_PROVEDORES -.->|testa| TEST_workspace_target_mesa_tests_config_test_mjs
  CMP_SONDA["CMP-SONDA<br/>sonda-corpo.mjs"]
  CMP_SONDA -->|realiza| CAP_SONDA
  CMP_SONDA -->|depende| CMP_AGENTE_API
  CMP_SONDA -->|depende| CMP_ORQUESTRADORA
  CMP_SONDA -->|depende| CMP_PROMPTS
  CMP_SONDA -->|depende| CMP_PROTOCOL
  CMP_SONDA -->|depende| CMP_PROVEDORES
  CMP_SONDA -.->|testa| TEST_workspace_target_mesa_tests_sonda_corpo_test_mjs
  CMP_VOO["CMP-VOO<br/>voo.js"]
  CMP_VOO -->|realiza| CAP_ORCH
  CMP_VOO -->|depende| CMP_CORE
  CMP_VOO -->|depende| CMP_DEMO
  CMP_VOO -->|depende| CMP_ORQUESTRADORA
  CMP_VOO -->|depende| CMP_PILOTO
  CMP_VOO -->|depende| CMP_PROTOCOL
  CMP_VOO -->|depende| CMP_PROVEDORES
  CMP_VOO -.->|testa| TEST_workspace_target_mesa_tests_voo_test_mjs
  IFC_CORE_API(["IFC-CORE-API<br/>Contrato do motor de estado (engine)"])
  CMP_CORE -.->|provê| IFC_CORE_API
  IFC_CORE_API -.->|consome| CMP_MESA
  IFC_CORE_API -.->|consome| CMP_PILOTO
  IFC_CORE_API -.->|consome| CMP_VOO
  IFC_CUSTO_CLI(["IFC-CUSTO-CLI<br/>Relatorio de custo via CLI"])
  CMP_CUSTO -.->|provê| IFC_CUSTO_CLI
  IFC_ORQ_PY_API(["IFC-ORQ-PY-API<br/>Orquestrador A2A em Python (CLI e classe)"])
  CMP_ORQ_PY -.->|provê| IFC_ORQ_PY_API
  IFC_PREFLIGHT_CLI(["IFC-PREFLIGHT-CLI<br/>Verificacao preflight via CLI"])
  CMP_PREFLIGHT -.->|provê| IFC_PREFLIGHT_CLI
  IFC_PROMPTS_API(["IFC-PROMPTS-API<br/>Montagem e orcamento do prompt"])
  CMP_PROMPTS -.->|provê| IFC_PROMPTS_API
  IFC_PROMPTS_API -.->|consome| CMP_MESA
  IFC_PROMPTS_API -.->|consome| CMP_PREFLIGHT
  IFC_PROMPTS_API -.->|consome| CMP_SONDA
  IFC_PROTOCOL_UTIL(["IFC-PROTOCOL-UTIL<br/>Contrato do protocolo de envelopes"])
  CMP_PROTOCOL -.->|provê| IFC_PROTOCOL_UTIL
  IFC_PROTOCOL_UTIL -.->|consome| CMP_CORE
  IFC_PROTOCOL_UTIL -.->|consome| CMP_PILOTO
  UI_MESA_CONFIG["UI-MESA-CONFIG"]
  UI_MESA_CONFIG -->|experiência| CAP_MESA
  UI_MESA_CONFIG -.->|satisfaz| REQ_010
  UI_MESA_LINHA["UI-MESA-LINHA"]
  UI_MESA_LINHA -->|experiência| CAP_MESA
  UI_MESA_LINHA -.->|satisfaz| REQ_011
  UI_MESA_PAINEL["UI-MESA-PAINEL"]
  UI_MESA_PAINEL -->|experiência| CAP_MESA
  UI_MESA_PAINEL -.->|satisfaz| REQ_012
  UI_MESA_TELEMETRIA["UI-MESA-TELEMETRIA"]
  UI_MESA_TELEMETRIA -->|experiência| CAP_MESA
  UI_MESA_TELEMETRIA -.->|satisfaz| REQ_013
  UI_MESA_TRANSITO["UI-MESA-TRANSITO"]
  UI_MESA_TRANSITO -->|experiência| CAP_MESA
  UI_MESA_TRANSITO -.->|satisfaz| REQ_003
  MET_COMPARABILIDADE[["MET-COMPARABILIDADE"]]
  MET_CONFORMIDADE[["MET-CONFORMIDADE"]]
  MET_RASTREABILIDADE[["MET-RASTREABILIDADE"]]
  REQ_001["REQ-001<br/>proposed"]
  REQ_001 -->|requisito| CAP_ORCH
  REQ_002["REQ-002<br/>proposed"]
  REQ_002 -->|requisito| CAP_ESTADO
  REQ_003["REQ-003<br/>proposed"]
  REQ_003 -->|requisito| CAP_MESA
  REQ_004["REQ-004<br/>proposed"]
  REQ_004 -->|requisito| CAP_DEMO
  REQ_005["REQ-005<br/>proposed"]
  REQ_005 -->|requisito| CAP_PREFLIGHT
  REQ_006["REQ-006<br/>proposed"]
  REQ_006 -->|requisito| CAP_CUSTO
  REQ_007["REQ-007<br/>proposed"]
  REQ_007 -->|requisito| CAP_SONDA
  REQ_008["REQ-008<br/>proposed"]
  REQ_008 -->|requisito| CAP_ORCH
  REQ_009["REQ-009<br/>proposed"]
  REQ_009 -->|requisito| CAP_ORCH
  REQ_010["REQ-010<br/>proposed"]
  REQ_010 -->|requisito| CAP_MESA
  REQ_011["REQ-011<br/>proposed"]
  REQ_011 -->|requisito| CAP_MESA
  REQ_012["REQ-012<br/>proposed"]
  REQ_012 -->|requisito| CAP_MESA
  REQ_013["REQ-013<br/>proposed"]
  REQ_013 -->|requisito| CAP_MESA
  RISK_ALIGN_001["RISK-ALIGN-001"]
  RISK_CHANGE_001["RISK-CHANGE-001"]
  RISK_CHANGE_002["RISK-CHANGE-002"]
  RISK_CONF_001["RISK-CONF-001"]
  RISK_CONF_002["RISK-CONF-002"]
  RISK_DECISION_001["RISK-DECISION-001"]
  RISK_DEP_001["RISK-DEP-001"]
  RISK_DERIV_001["RISK-DERIV-001"]
  RISK_DERIV_002["RISK-DERIV-002"]
  RISK_EXT_001["RISK-EXT-001"]
  RISK_INCUBA_001["RISK-INCUBA-001"]
  RISK_INGEST_001["RISK-INGEST-001"]
  RISK_INGEST_002["RISK-INGEST-002"]
  RISK_META_001["RISK-META-001"]
  RISK_META_002["RISK-META-002"]
  RISK_MOLD_001["RISK-MOLD-001"]
  RISK_ORIENT_001["RISK-ORIENT-001"]
  RISK_PRIV_001["RISK-PRIV-001"]
  RISK_PRIV_002["RISK-PRIV-002"]
  RISK_SEC_001["RISK-SEC-001"]
  RISK_STAGE_001["RISK-STAGE-001"]
  RISK_WEBQA_001["RISK-WEBQA-001"]
  ADR_001["ADR-001"]
  ADR_001 -->|mitiga| RISK_WEBQA_001
  ADR_002["ADR-002"]
  ADR_002 -->|mitiga| RISK_META_001
  ADR_003["ADR-003"]
  ADR_003 -->|mitiga| RISK_DEP_001
  ADR_004["ADR-004"]
  ADR_004 -->|mitiga| RISK_CHANGE_001
  ADR_005["ADR-005"]
  ADR_005 -->|mitiga| RISK_CONF_001
  ADR_006["ADR-006"]
  ADR_006 -->|mitiga| RISK_CONF_001
  ADR_006 -->|mitiga| RISK_STAGE_001
  ADR_007["ADR-007"]
  ADR_007 -->|mitiga| RISK_PRIV_001
  ADR_007 -->|mitiga| RISK_PRIV_002
  ADR_008["ADR-008"]
  ADR_008 -->|mitiga| RISK_DERIV_001
  ADR_008 -->|mitiga| RISK_DERIV_002
  ADR_009["ADR-009"]
  ADR_009 -->|mitiga| RISK_DERIV_002
  ADR_009 -->|mitiga| RISK_INGEST_001
  ADR_010["ADR-010"]
  ADR_010 -->|mitiga| RISK_INGEST_001
  ADR_010 -->|mitiga| RISK_INGEST_002
  ADR_011["ADR-011"]
  ADR_011 -->|mitiga| RISK_ALIGN_001
  ADR_012["ADR-012"]
  ADR_012 -->|mitiga| RISK_CONF_002
  ADR_012 -->|mitiga| RISK_DERIV_001
  ADR_013["ADR-013"]
  ADR_013 -->|mitiga| RISK_DEP_001
  ADR_013 -->|mitiga| RISK_SEC_001
  ADR_014["ADR-014"]
  ADR_014 -->|mitiga| RISK_META_001
  ADR_014 -->|mitiga| RISK_ORIENT_001
  ADR_015["ADR-015"]
  ADR_015 -->|mitiga| RISK_DERIV_001
  ADR_015 -->|mitiga| RISK_MOLD_001
  ADR_016["ADR-016"]
  ADR_016 -->|mitiga| RISK_CHANGE_001
  ADR_016 -->|mitiga| RISK_META_001
  ADR_017["ADR-017"]
  ADR_017 -->|mitiga| RISK_CONF_001
  ADR_017 -->|mitiga| RISK_DECISION_001
  ADR_018["ADR-018"]
  ADR_018 -->|mitiga| RISK_DEP_001
  ADR_018 -->|mitiga| RISK_SEC_001
  ADR_019["ADR-019"]
  ADR_019 -->|mitiga| RISK_CONF_001
  ADR_019 -->|mitiga| RISK_META_001
  ADR_020["ADR-020"]
  ADR_020 -->|mitiga| RISK_EXT_001
  ADR_020 -->|mitiga| RISK_META_002
  ADR_021["ADR-021"]
  ADR_021 -->|mitiga| RISK_META_001
  ADR_021 -->|mitiga| RISK_PRIV_001
  ADR_022["ADR-022"]
  ADR_022 -->|mitiga| RISK_META_001
  ADR_022 -->|mitiga| RISK_ORIENT_001
  ADR_023["ADR-023"]
  ADR_023 -->|mitiga| RISK_DEP_001
  ADR_023 -->|mitiga| RISK_META_001
  ADR_024["ADR-024"]
  ADR_024 -->|mitiga| RISK_CONF_001
  ADR_024 -->|mitiga| RISK_DEP_001
  ADR_025["ADR-025"]
  ADR_025 -->|mitiga| RISK_CONF_001
  ADR_025 -->|mitiga| RISK_EXT_001
  ADR_025 -->|mitiga| RISK_MOLD_001
  ADR_026["ADR-026"]
  ADR_026 -->|mitiga| RISK_CONF_001
  ADR_026 -->|mitiga| RISK_DERIV_002
  ADR_026 -->|mitiga| RISK_MOLD_001
  ADR_027["ADR-027"]
  ADR_027 -->|mitiga| RISK_CHANGE_001
  ADR_027 -->|mitiga| RISK_CHANGE_002
  ADR_028["ADR-028"]
  ADR_028 -->|mitiga| RISK_EXT_001
  ADR_028 -->|mitiga| RISK_META_002
  ADR_029["ADR-029"]
  ADR_029 -->|mitiga| RISK_EXT_001
  ADR_029 -->|mitiga| RISK_META_002
  classDef project fill:#1f2937,stroke:#111827,color:#fff;
  class PROJ_project_squadposlgpd project;
  classDef cap fill:#2563eb,stroke:#1e40af,color:#fff;
  class CAP_CUSTO,CAP_DEMO,CAP_ESTADO,CAP_MESA,CAP_ORCH,CAP_PREFLIGHT,CAP_SONDA cap;
  classDef cmp fill:#0891b2,stroke:#0e7490,color:#fff;
  class CMP_AGENTE_API,CMP_CORE,CMP_CUSTO,CMP_DEMO,CMP_MESA,CMP_ORQ_PY,CMP_ORQUESTRADORA,CMP_PILOTO,CMP_PREFLIGHT,CMP_PROMPTS,CMP_PROTOCOL,CMP_PROVEDORES,CMP_SONDA,CMP_VOO cmp;
  classDef ifc fill:#7c3aed,stroke:#5b21b6,color:#fff;
  class IFC_CORE_API,IFC_CUSTO_CLI,IFC_ORQ_PY_API,IFC_PREFLIGHT_CLI,IFC_PROMPTS_API,IFC_PROTOCOL_UTIL ifc;
  classDef rule fill:#16a34a,stroke:#15803d,color:#fff;
  classDef ui fill:#db2777,stroke:#9d174d,color:#fff;
  class UI_MESA_CONFIG,UI_MESA_LINHA,UI_MESA_PAINEL,UI_MESA_TELEMETRIA,UI_MESA_TRANSITO ui;
  classDef req fill:#0d9488,stroke:#0f766e,color:#fff;
  class REQ_001,REQ_002,REQ_003,REQ_004,REQ_005,REQ_006,REQ_007,REQ_008,REQ_009,REQ_010,REQ_011,REQ_012,REQ_013 req;
  classDef met fill:#ea580c,stroke:#c2410c,color:#fff;
  class MET_COMPARABILIDADE,MET_CONFORMIDADE,MET_RASTREABILIDADE met;
  classDef test fill:#57534e,stroke:#44403c,color:#fff;
  class TEST_workspace_target_mesa_tests_aceite_test_mjs,TEST_workspace_target_mesa_tests_agente_api_test_mjs,TEST_workspace_target_mesa_tests_config_test_mjs,TEST_workspace_target_mesa_tests_custo_test_mjs,TEST_workspace_target_mesa_tests_degeneradas_test_mjs,TEST_workspace_target_mesa_tests_e2e_test_mjs,TEST_workspace_target_mesa_tests_engine_test_mjs,TEST_workspace_target_mesa_tests_entrega_test_mjs,TEST_workspace_target_mesa_tests_espelho_guarda_test_mjs,TEST_workspace_target_mesa_tests_frescor_test_mjs,TEST_workspace_target_mesa_tests_orquestrador_py_test_mjs,TEST_workspace_target_mesa_tests_orquestradora_test_mjs,TEST_workspace_target_mesa_tests_piloto_tela_test_mjs,TEST_workspace_target_mesa_tests_piloto_test_mjs,TEST_workspace_target_mesa_tests_preflight_test_mjs,TEST_workspace_target_mesa_tests_prompt_contrato_test_mjs,TEST_workspace_target_mesa_tests_prompts_agentes_test_mjs,TEST_workspace_target_mesa_tests_protocol_test_mjs,TEST_workspace_target_mesa_tests_real_deepseek_test_mjs,TEST_workspace_target_mesa_tests_sonda_corpo_test_mjs,TEST_workspace_target_mesa_tests_telemetria_test_mjs,TEST_workspace_target_mesa_tests_voo_demonstracao_test_mjs,TEST_workspace_target_mesa_tests_voo_test_mjs,TEST_workspace_target_src_orquestrador_a2a_py,TEST_workspace_target_tests_test_orquestrador_a2a_py test;
  classDef adr fill:#ca8a04,stroke:#a16207,color:#fff;
  class ADR_001,ADR_002,ADR_003,ADR_004,ADR_005,ADR_006,ADR_007,ADR_008,ADR_009,ADR_010,ADR_011,ADR_012,ADR_013,ADR_014,ADR_015,ADR_016,ADR_017,ADR_018,ADR_019,ADR_020,ADR_021,ADR_022,ADR_023,ADR_024,ADR_025,ADR_026,ADR_027,ADR_028,ADR_029 adr;
  classDef risk fill:#dc2626,stroke:#991b1b,color:#fff;
  class RISK_ALIGN_001,RISK_CHANGE_001,RISK_CHANGE_002,RISK_CONF_001,RISK_CONF_002,RISK_DECISION_001,RISK_DEP_001,RISK_DERIV_001,RISK_DERIV_002,RISK_EXT_001,RISK_INCUBA_001,RISK_INGEST_001,RISK_INGEST_002,RISK_META_001,RISK_META_002,RISK_MOLD_001,RISK_ORIENT_001,RISK_PRIV_001,RISK_PRIV_002,RISK_SEC_001,RISK_STAGE_001,RISK_WEBQA_001 risk;
```
