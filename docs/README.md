# Docs


Project notes and runbooks, to be migrated here from the loose markdown files.


********************************************************************************

## To migrate


| Source | Target | Notes |
| --- | --- | --- |
| `website/Hirement_website_notes.md` | `docs/website/` | 3k+ lines, chronological. Split by topic: hosting, deploy, DNS and SSL, DB, content model, MCP. |
| `notes/Hirement_Dev_Notes.md` | `docs/dev/` | Short, recent. |
| `Hirement_notes.md` (business) | `docs/business/` | Full of live credentials. Strip every password, key and token, and replace with a pointer to where it lives. |

Sources sit outside this repo. Don't open them without being asked; see the
scope rule in `.claude/CLAUDE.md`.


********************************************************************************

## Rule


Nothing lands here until credentials are stripped. Where a note references a
secret, write what it is and where to find it, never the value.
