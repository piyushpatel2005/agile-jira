# Agile with Atlassian Jira

This repository includes documents for learning Jira and working in Agile environment.


Quick search allows to search text based search for issues, backlog, etc. It is on left blue background. Basic search is at the top. Advanced search are possible using Jira Query language (JQL). We can also filter issues on Contextual menu on left side.

`feature NOT 1` shows issues with 'feature' word but not '1'. We can also include multiple terms using `AND`. We can use `OR` or wildcard character.


### JQL

When we go to advanced search the text box is populated as `order by created DESC` which is JQL. It allows for powerful searches. For automation with JIRA also, we need JQL.
We can find advanced searching on search engine as "Advanced Searching - field options" which points to Atlassian documentation.

```sql
-- search given project
project = PROJ order by created DESC
-- order by summary and key
ORDER by summary ASC, key
<fieldname> <operator> <field value>
-- Jira also has few functions
assignee = currentUser()
created > startOfDay()
created > -2d -- created in last 2 days (48 hours)
-- (+/-)nn(y|M|w|d|h|m)
created > -2h -- created in last two hours
created > startOfDay(-2d) -- created since start of day 2 days ago
created > startOfMonth(+14d) -- created since the 15th of this month
"Story Points" >= 3
project in (projectA, projectB)
project not in projectA
assignee is EMPTY
assignee = EMPTY
summary ~ "feature 1"
summary !~ feature -- quotes not required for single word
-- issues where the current user has been assigned
assignee was currentUser()
-- issues that have never had a status of In Progress
status was not "In Progress"
status was in ("Selected for Development", "In Progress")
status was not in ("Selected for Development", "In Progress")
-- find all issues moved to Done status by the current user in the past month
status was Done BY currentUser() AFTER -1M
-- AFTER "Date"
-- BEFORE "date"
-- DURING ("date1", "date2")
-- ON "date"
-- BY "username"
-- FROM "oldvalue"
-- TO "newvalue"
-- Find issues whose status changed from Done to In Progress in history.
status changed FROM "Done" TO "In Progress"

--
assignee = currentUser() AND status = "In Progress"
status = "Selected for Development" OR status = "In Progress"
status in ("Selected for Development", "In Progress")

NOT status = backlog
status != Backlog
-- find unresolved issues in all projects except projectA
resolution = Unresolved AND NOT project = projectA
-- change priority by using parentheses
summary = "feature" AND (status = "Selected fro Development" OR status = "To Do")
-- AND has higher precedence over OR
```

There are many advanced search  functions. like startOfDay(), startOfWeek, startOfMonth, endOfDay, endOfYear, now, currentLogin, lastLogin, etc.

There are operators:

EQUALS (=)
NOT Equals (!=)
Greater than (>)
Less than (<)
Less than or equal to (<=)
in
contains (~)
does not contain (!~)

There are also boolean operators AND, OR and NOT.
