# Sync Address Database

Keeps the Postgres address table in step with the master address sheet. This is the
reference list that Find Address searches.

## What happens
1. Started by hand, when the address sheet has been updated.
2. **Fetch All Sheet Rows** reads the whole column of raw address lines.
3. **Parse Sheet Rows** splits each line into company, street, city, state and zip.
4. **Batch 200 at a Time** sends them in batches instead of one enormous request.
5. **Insert Batch** upserts each batch: rows already there are skipped, not duplicated,
   so the sync can be run as often as you like.

## Decisions worth pointing out
- **The zip is read from the end of the line, not the first five digits found.** Street
  numbers are five digits too, and taking the first match filed the wrong value.
- **Duplicates are handled by the database**, on a unique address column, rather than by
  code trying to remember what it has seen.
- The full code is published here, because this part has no client-specific logic in it.

## What is in this folder

`workflow.json` is a cleaned copy of the live workflow. Every step, every connection and
every setting is real. The code inside the steps is replaced by a note, and the comments
above each step are kept, because those explain the thinking. Logins, keys, web addresses,
sheet and database IDs, client names and real job links are removed.
