# Daily Task Tracker

A single-page task tracker (Sno, Task, Priority, Status) hosted on GitHub Pages, with data stored in `tasks.json` in this repo.

## Live app
`index.html` fetches `tasks.json` on load. Filter by priority/status, search by text, sort by clicking any column header, edit a task by clicking its text, change priority/status inline, add a row from the top bar, delete with the X button.

## Saving changes back to GitHub
GitHub Pages is static, so writes go through the GitHub Contents API:

1. Click the settings (gear) icon.
2. 2. Enter your GitHub username/org, repo name, branch (main), file path (tasks.json), and a fine-grained Personal Access Token scoped to only this repo with Contents: Read and write permission.
   3. 3. Click Save settings, then Save to GitHub any time you want to commit your edits.
     
      4. Create a token at: Settings > Developer settings > Personal access tokens > Fine-grained tokens. The token is stored only in your browser's localStorage and is sent only to api.github.com.
     
      5. Until you click "Save to GitHub," edits live in your browser (localStorage) so refreshing won't lose them, but other devices/collaborators won't see them.
     
      6. ## Suggestions / possible upgrades
      7. - Due dates: add a dueDate field plus a "Due soon / overdue" filter, most task trackers need this.
         - - Multi-user safety: the current save flow can silently overwrite a teammate's concurrent edit. A GitHub Action that validates the JSON on push would catch corruption early.
           - - Auth via GitHub OAuth App instead of a manually pasted PAT, removes the copy/paste step and lets you scope permissions per user, at the cost of needing a small backend to handle the OAuth token exchange.
             - - Notifications: a scheduled GitHub Action that opens an issue or sends a Slack/email digest of overdue tasks.
               - - Better source of truth: if this grows past personal use, a real datastore (Airtable, Google Sheets, or a small database) with the same UI would scale better than committing JSON on every edit.
                 - - History/undo: since every save is a git commit, you already get free version history in the repo's commit log.
                   - 
