# Nightshift — {{date}}

*{{count}} papercuts fixed overnight.*

{{#each items}}
- <{{pr_url}}|#{{pr_number}}> {{title}} — {{one_line_risk}}
  `{{files_changed}} files` · tests: {{checks_passed}}/{{checks_total}} passed
{{/each}}

*Undo:* `/nightshift undo {{run_id}}`
*Next run:* {{next_run}}
