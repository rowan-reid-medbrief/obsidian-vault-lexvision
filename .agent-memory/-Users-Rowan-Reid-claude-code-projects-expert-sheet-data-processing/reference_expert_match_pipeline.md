---
name: reference-expert-match-pipeline
description: "Corroborated end-to-end Expert Match data pipeline (expert_match source repo): how researched profiles reach the product"
metadata: 
  node_type: memory
  type: reference
  originSessionId: 32ef5056-c8d8-4a67-9052-1763194c8825
---

## Expert Match data pipeline (corroborated from source, 2026-06-01)

Source: Azure DevOps `MedBrief AI` / `expert_match` repo (read directly). How Laura's
researched expert profiles reach the Expert Match product:

1. **Generate** — `rnd/expert_data_collection/gemini_file.py`: per expert, Gemini + Google
   Search returns a structured profile (specialty, qualifications, career history, etc.)
   against the controlled specialty list + `profile_score`. Output = the
   `experts_AI_prefilled (251010)` sheet of `expert_data_collection_v2_07-25.xlsx`.
2. **Filter** — `production_main.py` `filter_experts`: keeps rows where `expert=='expert'`
   AND `Status=='done'`, drops agency domains.
3. **Clinician QA** — merges `Clinician_QA_Template...` / sheet `Expert_Specialities_QA`.
4. **Rephrase + transform** — `main_rephrase`, then `transform_expert_csv.py`
   `main_transform_schema`: emits the Expert schema; resolves each row to a `fos_user`
   `expert_id` (email then name lookup); normalises specialties.
5. **Ingest** — `src/storage_app/storage_init/__init__.py` `add_expert_data_sql_vector_db`:
   upserts into `[dbo].[Expert]` SQL table AND embeds into the `expert-search-index` Azure
   Cognitive Search vector store. (`storage_update` does live updates.)
6. **Serve** — `src/expert_search_service` (`POST /search_experts_service`): hybrid
   dense+full-text RAG over `expert-search-index` with RRF + LLM justifications, for
   solicitors searching experts.

Key facts: the shared join key throughout is `expert_id` = `fos_user.id`; `AZURE_SHARE_NAME`
defaults to `expert-match`. This enrichment is for ALREADY-confirmed experts (display/search)
and is DISTINCT from Rowan's Phase 1 classification (deciding WHICH fos_user rows are medical
experts). See [[project-profile-generation]].
