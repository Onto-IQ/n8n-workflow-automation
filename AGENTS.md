# AGENTS.md

Working notes for coding agents in this repository. `CONTRIBUTING.md` is the
authoritative source for the structure rules summarised here.

## What this repo is

**Workflow Automation with n8n — L1**: an Onto-IQ training course with 27 units,
written in Thai with English commands and tool names. Every unit pairs a lesson
(theory) with an exercise (hands-on lab). The repo also ships 25 runnable n8n
workflow JSON files and a self-hosting Docker stack.

It is course material, not an application. There is no build, typecheck, linter,
formatter, package manifest, dependency install or test suite. The only
automated check is a folder-structure script.

## Layout

```text
README.md COURSE.md SETUP.md CONTRIBUTING.md CHANGELOG.md
lessons/NN-slug/      README.md                                  theory (full chapter, one file)
exercises/NN-slug/    README.md + LAB.md + starter/ + solution/  hands-on; solution/ holds workflow .json
org/                  topic-family notes (onto-iq.md, datafabric-academy.md)
other/                everything that is not a lesson or exercise
  assets/ datasets/ docs/ reference/ scripts/ slides/
  docs/ holds INSTRUCTOR.md, JD.md and credentials/
docker-compose.yml    n8n + postgres + cloudflared
.env.example          copy to .env before `docker compose up`
```

## Commands

```bash
bash other/scripts/check_structure.sh   # the only check; run from the repo root
```

CI (`.github/workflows/structure-check.yml`) runs the same script on every push
and pull request. Run it before finishing any change that adds, moves or renames
files. The scripts are not executable: call them with `bash` / `python`.

Self-hosted n8n (needs `.env` first):

```bash
cp .env.example .env                    # set POSTGRES_PASSWORD, N8N_HOST, WEBHOOK_URL, CLOUDFLARE_TUNNEL_TOKEN
docker compose up -d                    # editor at http://localhost:5678
docker compose logs -f n8n
docker compose down
docker compose pull && docker compose up -d            # upgrade n8n
docker compose exec n8n n8n user-management:reset     # forgot password
cp -r data data-backup-$(date +%Y%m%d)  # back up
```

- `data/postgres/` and `data/n8n/` are git-ignored bind mounts. `data/n8n/` holds
  the encryption key for stored credentials: never delete `data/`, and back up
  both folders together.
- `WEBHOOK_URL`, `N8N_HOST` and `CLOUDFLARE_TUNNEL_TOKEN` have no defaults.
- `WEBHOOK_URL` must be a full `https://` URL. Production webhooks (LINE,
  Telegram, GitHub) and n8n chat features need HTTPS, which the Cloudflare
  Tunnel provides. The editor is used at `http://localhost:5678`.
- The stack does not load this repo's workflows. Import is manual: paste the
  JSON onto the n8n canvas, or Workflow → Import from File / URL.
- Nothing validates workflow JSON. After editing one, parse it to confirm it is
  still valid JSON.

## Structure rules (enforced by `other/scripts/check_structure.sh`)

- Units come in pairs with the same folder name: `lessons/NN-slug/` and
  `exercises/NN-slug/`. Names must match `^[0-9]{2}-[a-z0-9]+(-[a-z0-9]+)*$`.
- A lesson folder needs `README.md` only (the full lesson chapter, merged
  self-study style). An exercise folder needs
  `README.md`, `LAB.md`, `starter/` and `solution/`. Keep empty `starter/` and
  `solution/` folders with a `.gitkeep`.
- The root docs, `org/`, `other/` and its subfolders are required by name.
  Don't rename or move them.
- `COURSE.md` front matter is the machine-readable contract. If you move a
  folder, update the matching `*_path` field.

## Conventions (not enforced by the script)

- Never add a top-level folder. Supporting material goes under `other/`.
- Thai filenames are allowed only under `other/`, never in `lessons/` or
  `exercises/`.
- Prose is Thai; commands, tool names and code are English.
- Each lesson cites its slide range from the deck in `other/slides/` in the
  header table of `lessons/NN-slug/README.md`, and its content must agree with
  the deck.
- No secrets (`.env`, API keys) and no file over 100 MB. Link large binaries
  from `other/datasets/README.md` instead.
- Content must not carry the former training company's branding or copyright
  marks (`org/onto-iq.md`).
- When you add, rename or remove a `solution/*.json`, update every place that
  names it: the `ไฟล์ workflow สำเร็จรูป:` list in the exercise `README.md`
  and any `LAB.md` that refers to it. A new unit also needs a
  row in the root `README.md` outline.

All 27 units share one file template. Copy an existing unit when adding one.

| File | Sections, in order |
|---|---|
| `lessons/NN-slug/README.md` | title `# NN — topic`, table (lesson, exercise, time, slide range), intro paragraph, content sections (topic-named), Demo / walkthrough, Key takeaways, ลงมือทำ, Check understanding, Next (paired exercise + next unit) |
| `exercises/NN-slug/README.md` | link to the paired lesson, table (LAB, starter, solution), `ไฟล์ workflow สำเร็จรูป:` list, Goal, Before you start |
| `exercises/NN-slug/LAB.md` | Goal, Setup (numbered steps), Check your work, Stretch (optional) |

## Workflow JSON (`exercises/NN-slug/solution/*.json`)

- Target version is n8n 2.48.5 (bumped from 2.28.6 so the Agents feature of
  unit 26 is available; self-hosted Agents need n8n ≥ 2.32.3), pinned in
  `docker-compose.yml` and quoted in `other/reference/n8n-2026-rebrand-and-2x.md`.
- Format: UTF-8 without BOM, 2-space indent, one key per line, literal Thai and
  emoji (no `\uXXXX` escapes), trailing newline. That is
  `json.dumps(workflow, indent=2, ensure_ascii=False) + "\n"`. `name` is the
  first key.
- Two styles coexist: n8n exports (`pinData`, `versionId`, `meta`, `id`, `tags`)
  and hand-authored minimal files. Match the file you are editing and leave the
  others alone.
- Node versions the repo was migrated to; treat them as minimums: Set 3.4, IF
  2.3, AI Agent 3.1, Chat Trigger 1.4, Memory Buffer Window 1.3, Split Out 1,
  Message an Agent 3.1. `itemLists` is no longer used.
  `other/scripts/migrate_workflows_2_28_6.py` shows the exact parameter shapes.
- On n8n 2.48.5 the Execute Workflow Trigger (1.1) requires
  `parameters.workflowInputs.values` (field name + type per input). The legacy
  shape (`{"event": "onReceived"}` only) still imports but the sub-workflow
  refuses to execute ("At least 1 field is required"). The 05B-Sub files and
  `26-agents`' FAQ tool carry the new shape; its field names must match the
  `workflowInputs.mapping` of the caller (`toolWorkflow` / Execute Sub-workflow).
- Any value containing `{{ }}` must start with `=`, as in `"={{ $json.chatInput }}"`.
  Without the `=`, n8n sends the text literally.
- Credentials are placeholders:
  `"credentials": { "<type>": { "id": "YOUR_<SERVICE>_CREDENTIAL", "name": "…" } }`,
  and resource ids are `YOUR_<THING>_ID`. Never put keys or tokens in JSON; use
  n8n's credential store.
- A node `name` is the join key. It appears in `connections` keys, in link
  targets and in `$('Node Name')` expressions, so rename it in all of them at
  once.
- 17 of the 22 pre-2.48.5 files have no top-level `id`; n8n creates one on
  import. Don't invent ids. (The unit 26–27 files are hand-authored in the same
  minimal style — also no top-level `id`, 20 of 25 in total.)
- LINE workflows need the community node `@aotoki/n8n-nodes-line-messaging`,
  which the Docker stack does not preinstall.
- `04 - MCP Client.json` hard-codes an external MCP endpoint
  (`https://n8n.datafabric.app/mcp/mcp1`).
- Filenames contain spaces, `&` and parentheses. Quote them in shell commands.

## Gotchas

- The maintainer's checkout has a local-only, git-ignored generator,
  `_tools/build_structure.py`. When run, it rewrites all lesson and exercise
  Markdown files, the deck, `check_structure.sh` and both CI YAML files, which
  overwrites hand edits to those files — as of the LESSON.md merge it would also
  resurrect the two-file README+LESSON layout and recreate `LESSON.md` files.
  Do not run it without updating it first.
- `other/scripts/migrate_workflows_2_28_6.py` is a stale one-off. Its
  `WORKFLOWS_DIR` resolves to `other/workflows`, which no longer exists, so it
  does nothing. If you repoint and re-run it, it rewrites workflow files in
  place and gives new UUIDs to any node it migrates.
- The real node-schema migration is commit `096cf77`. Commit `8b154da` is titled
  "Refactor workflow node schemas" but only adds dataset files. The old
  `workflows/` tree and its READMEs are in history up to `8b154da`.
- The docs say there are 18 solution workflows. There are 24.
- There is no `.gitattributes`. The maintainer's Windows checkout has
  `core.autocrlf=true`, so working-tree text files are mostly CRLF while the
  repo stores LF. Git normalises on commit, so leave line endings alone.
- The repo's `.gitignore` does not cover `.cursor/`, although `.env.example`
  says to put an n8n API key in `.cursor/mcp.json`. In the maintainer's checkout
  it is ignored only by a global gitignore, so in a fresh clone that file could
  be committed.
- The maintainer's checkout holds more than 1 GB of git-ignored local files
  (`_tools/`, `_deck_inspect/`, root `*.pptx`). Exclude them from recursive
  searches.

## Known defects in existing content

Verified in the files. Don't copy these patterns, and fix them only when asked.

- `exercises/05-loops/solution/03-Flow-Control-Demo-Loop-V2.json` has no Loop
  node, although unit 05's `LAB.md` tells learners to import it. The working
  loop is in `03-Flow-Control-Demo-Loop.json`.
- `exercises/23-multi-agents/solution/05B - Orchestration Multi-Agent Refund & Claim.json`
  points its four `toolWorkflow` nodes at the `05B-Sub-*.json` files by id, but
  those files carry no top-level `id`. Each must be re-selected in n8n after
  import.
- Values with `{{ }}` but no leading `=`: in the unit 10 Form workflow,
  `Create Calendar Event` (`summary`, `description`) and `Create Google Doc`
  (`content`); in the unit 13 Candidate Screening workflow, `Send Confirmation
  Email` (`subject`, `message`).
- In the unit 10 Form workflow, `LINE Push Message` reads
  `$('Line Messaging Trigger')`, a node that does not exist there.
- Every `LAB.md` has generator artefacts: the `Stretch (optional)` bullet is a
  Python list literal (`- ['…', '…']`) and the `Setup` numbering restarts after
  two fixed steps.

## Read before editing

| Changing | Read first |
|---|---|
| Units, folders, course metadata | `CONTRIBUTING.md`, `COURSE.md` |
| Lesson or exercise content | `other/docs/INSTRUCTOR.md` (it lists the pitfalls the course deliberately plants; don't fix them out), then the unit's lesson `README.md` and the paired `LAB.md` |
| Workflow JSON or n8n-version-specific text | `other/reference/n8n-2026-rebrand-and-2x.md`, `other/docs/credentials/README.md` |
| `docker-compose.yml`, `.env.example` | `SETUP.md`, `lessons/25-self-hosting/` |
| Course description | `other/docs/JD.md`. Its source of truth is an Obsidian file outside the repo (`jd_source` in `COURSE.md`). |
