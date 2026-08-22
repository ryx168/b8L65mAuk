# xotours-db backups

Dedicated, standalone repo whose only job is backing up and restoring the
`xotours-db` Cloudflare D1 database. Kept separate (and public, for free
unlimited Actions minutes) from the main application repo on purpose, since
that repo's git history contains sensitive data unrelated to this task.

## Setup (one-time)

Add these repository secrets under Settings -> Secrets and variables ->
Actions:

- `CLOUDFLARE_API_TOKEN` - a token scoped to D1 read/write on the account
  that owns `xotours-db`
- `CLOUDFLARE_ACCOUNT_ID` - that account's ID

## Usage

- **Backup**: runs automatically daily at 9am UTC, or trigger manually from
  the Actions tab ("D1 Database Backup" -> Run workflow). Output lands in
  `d1_backups/`, keeping the newest 30 files.
- **Restore**: Actions tab -> "D1 Database Restore" -> Run workflow, pick a
  backup filename from `d1_backups/`, and type `RESTORE` to confirm. Takes
  a fresh safety snapshot of the live database first, then overwrites it
  with the selected backup.
