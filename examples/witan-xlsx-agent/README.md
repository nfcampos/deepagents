# Witan XLSX Agent

Use [Deep Agents CLI](https://github.com/langchain-ai/deepagents) with
[Witan Headless Excel](https://github.com/witanlabs/witan-cli) to inspect and modify Excel
workbooks, including creating new ones from scratch.

This example shows how to add spreadsheet support to a Deep Agents project with
a project-local skill. It does not require any custom middleware or SDK
wrappers.

## What It Enables

With this example installed, Deep Agents can use Witan to work with Excel files
such as `.xls`, `.xlsx`, and `.xlsm`:

- create new `.xlsx` workbooks from scratch
- inspect workbook structure and list sheets
- read cells, rows, columns, and ranges
- trace formulas and dependencies
- run what-if analysis
- make workbook edits and save them back to disk when needed

## Prerequisites

- `uv`
- a Witan account
- authentication via `WITAN_API_KEY` or `witan auth login`

## Install

```bash
uv tool install deepagents-cli
uv tool install witan
```

Authenticate with either:

```bash
export WITAN_API_KEY="..."
```

or:

```bash
witan auth login
```

## Run It

This example does not include a workbook. Run Deep Agents from a directory that
contains the workbook you want to inspect, or reference the workbook by path.

```bash
cd examples/witan-xlsx-agent
deepagents --skill xlsx-code-mode -m "Open ./report.xlsx and summarize the key drivers."
```

You can also start a normal Deep Agents session and mention the workbook in
your request:

```bash
deepagents
```

Example prompts:

- `Create a new workbook called budget.xlsx with sheets for Inputs, Summary, and Assumptions.`
- `Open ./financial-model.xlsx and tell me which sheets feed the summary tab.`
- `Trace the inputs that drive Summary!C18.`
- `Compare Output!C30 when Inputs!B5 is 0.02, 0.04, and 0.06.`

## Add It To Your Own Project

Copy the `.deepagents` folder into your project:

```bash
cp -R examples/witan-xlsx-agent/.deepagents /path/to/your-project/.deepagents
cd /path/to/your-project
deepagents
```

Once the skill is present and `witan` is installed, Deep Agents can load the
spreadsheet workflow from your project automatically.

## Project Layout

```text
witan-xlsx-agent/
└── .deepagents/
    ├── AGENTS.md
    └── skills/
        └── xlsx-code-mode/
            └── SKILL.md
```

## How It Works

- Deep Agents discovers the skill from `.deepagents/skills/xlsx-code-mode/`
- The skill instructs the agent to use `witan xlsx exec` for spreadsheet work, including new workbook creation
- Witan handles workbook access, calculation, and edits
