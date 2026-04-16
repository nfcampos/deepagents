# Witan Spreadsheet Agent

You have access to the `xlsx-code-mode` skill.

Use it whenever the task involves an Excel workbook (`.xls`, `.xlsx`, `.xlsm`)
or the user asks you to inspect, explain, calculate, or modify a spreadsheet.

Do not try to inspect workbook bytes with plain text tools. Prefer batching
related spreadsheet work into a single `witan xlsx exec` call when that keeps
the workflow clear.

When you change a workbook, be explicit about whether the operation is read-only
or whether you are persisting changes with `--save`.
