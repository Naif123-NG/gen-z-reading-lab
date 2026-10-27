# Gen Z Reading Lab

Single-file reading site for students (`index.html`). Hosted on GitHub Pages; settings and student data live in Supabase.

## What is stored where

| Thing | Where | Who can change it |
|---|---|---|
| Which readings are locked, starting level | Supabase table `rl_settings` | Teacher, from `#/teacher`, with the dashboard PIN |
| Student topic suggestions | Supabase table `rl_suggestions` | Students add; teacher reads and deletes from `#/teacher` |
| Student scores and every answer (one row per student ID, device key `student:<ID>`) | Supabase table `rl_results` | Students write their own; teacher reads and deletes from `#/teacher` (`rl_admin_delete_results`) |
| Visitor counter | Supabase function `rl_hit` | Automatic |

Supabase project: `rhcjdcwvndbhrbwatgoy` (same project as the other classroom pages). The new tables are closed to direct access.
Everything goes through functions: `rl_get_settings`, `rl_suggest`, `rl_save_results` (students) and
`rl_admin_check`, `rl_admin_set`, `rl_admin_suggestions`, `rl_admin_delete_suggestions`, `rl_admin_results` (PIN checked).

The teacher PIN is the same one used by the lesson and review dashboards (`_lesson_check_pin`). Ten wrong tries lock every
dashboard for 15 minutes, so type it carefully.

## How students get changes

The page asks Supabase for the lock list every 8 seconds, and again whenever the tab regains focus.
When the teacher unlocks a reading, students see it open within a few seconds, with no reload.
The footer shows "Teacher settings live" or a warning if the page cannot reach Supabase.

## Changing the page

1. Edit `index.html`.
2. Commit and push in GitHub Desktop. Pages updates in about a minute.
3. Students should hard-refresh (Ctrl+Shift+R) if an old tab is still open.

## Teacher

Open `https://<your-pages-address>/#/teacher`, enter the PIN, and use the lock buttons.
Suggestions and student results are listed lower on the same page.
