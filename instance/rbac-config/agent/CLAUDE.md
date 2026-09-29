## Jira issue creation

Whenever this instance creates a Jira issue, set its **Team** field to **Console Access** in the `jira_create_issue` call. Resolve the Team custom-field ID and required value format from Jira field options or an existing issue, then include it in the `additional_fields` JSON alongside any other required fields. If needed, find an existing RHCLOUD issue with Team = Console Access using `jira_search`, inspect it with `jira_get_issue(fields="*all")`, and reuse the Team custom-field key and value shape; confirm the option with `jira_get_field_options` when available. Do not create the issue without the Team value; if it cannot be set, report the blocker.

## Pull request titles

Every GitHub PR created by this instance MUST have a title matching `[PROJECT-12345]: <title>`: uppercase Jira project key, numeric issue key, a colon, one space, and a non-empty title. Before calling `gh api .../pulls` or another PR creation command, validate the title against `^\[[A-Z][A-Z0-9]*-\d+\]: \S(?:.*\S)?$`. Use the Jira issue assigned to the work. Do not create the PR if its title is invalid or if no Jira key is available; never invent a key.
