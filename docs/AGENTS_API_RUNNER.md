# Official Agents API runner - implemented, not live-tested

## Current status (2026-10-30 KST)

The supplied Studio URL is
`https://studio.upstage.ai/agents/agt_bXRXFSAqFmBayPjZF7VgRQ`.
Opening it in the connected in-app browser returned Studio's own 404 screen.
Refreshing a previously bound tab separately failed with `browser.user is unavailable`.
We cannot determine whether the 404 is caused by an unavailable workflow or the
connected account's permissions. No native nodes have been inspected or configured.

The existing three C001 PDFs and manifest hashes were checked in the offline
preflight. The environment has no `UPSTAGE_API_KEY` and no optional OpenAI SDK.
**No API upload or Studio execution has been performed.**

## Run the preflight (no network)

```powershell
python scripts/run_studio_agent.py --agent-id agt_bXRXFSAqFmBayPjZF7VgRQ --pdf data/cases/SYN-C001/SYN-C001_purchase_order.pdf data/cases/SYN-C001/SYN-C001_delivery_notice.pdf data/cases/SYN-C001/SYN-C001_quotation.pdf --preflight
```

The report checks PDF headers, duplicate files, filenames and SHA-256, plus whether
the credential and SDK are available. It does not validate agent access, workflow
configuration, or document extraction accuracy.

## Run the real API when access is available

Install optional dependencies with `python -m pip install -r requirements-agents.txt`.
Configure `UPSTAGE_API_KEY` in the local environment without including it in chat,
command arguments, commits, logs or artifacts. The script does not create a key.
Verify the workflow in Studio first; its configuration is still unverified here.

```powershell
python scripts/run_studio_agent.py --agent-id agt_bXRXFSAqFmBayPjZF7VgRQ --pdf data/cases/SYN-C001/SYN-C001_purchase_order.pdf data/cases/SYN-C001/SYN-C001_delivery_notice.pdf data/cases/SYN-C001/SYN-C001_quotation.pdf --output data/results/studio_runs/UNIQUE_RUN_ID --config-version ACTUAL_CONFIG_VERSION --prompt-version ACTUAL_PROMPT_VERSION
```

The runner uses the fixed official `https://api.upstage.ai/v2` endpoint, uploads
each source PDF with `purpose=user_data`, and supplies all file IDs in a single
Responses job. It polls `queued`/`in_progress` with bounded intervals and saves
final output plus `include=all` step history. Snapshots are serialized SDK response
objects, not raw HTTP wire bytes.

The destination must not already exist. It archives copies of the source PDFs,
upload replies, the exact job request, job snapshots, job ID, prompt/config versions
and source hashes. API results use `execution_mode=live_agents_api`; fake-client
tests use `contract_test`. No gold or synthetic output replaces an API failure.

The SDK client disables automatic retries. If a submit call times out, the server
may have accepted it without returning an ID. Check job history before retrying.
Polling timeout does not cancel the server job. Failed or incomplete runs retain
their available snapshots and report `NEEDS_REVIEW`. Error class/HTTP status may be
recorded; exception text is not blindly saved because it can contain request data.
Uploaded files are not automatically deleted, preserving review evidence.

## Hand off the actual final output to the existing engine

```powershell
python scripts/analyze_studio_export.py --export data/results/studio_runs/UNIQUE_RUN_ID/studio_final.json --base data/cases/SYN-C001/trusted_base_case.json --output data/results/studio_runs/UNIQUE_ANALYSIS_ID --run-id ACTUAL_JOB_ID --config-version ACTUAL_CONFIG_VERSION --prompt-version ACTUAL_PROMPT_VERSION
```

The existing normalized contract must be present in the final output. Unsupported
native formats are rejected until real response data establishes their mapping.
Transport success does not prove correct extraction. `evidence_verified_against_pdf`
remains false; original PDF evidence must be reviewed separately.

## Validation and limits

Local Python 3.13.9: **61 tests passed**, Ruff passed. The 13 added tests use a fake
client and cover one-job grouping, source archives, failure retention, unknown
submit outcomes, polling deadlines, duplicate inputs, invalid files/agent IDs and
output overwrite prevention. The actual optional SDK and live service have not
been exercised in this environment. These are transport contract regressions,
not measured Studio performance. Existing engine and adapter were not rewritten.

Official sources checked on 2026-10-30:

- https://console.upstage.ai/docs/agents
- https://console.upstage.ai/docs/agents/files
- https://console.upstage.ai/docs/agents/jobs
