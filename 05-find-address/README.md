# Find Address

Fills in the exact street address on records the scraper could not complete.

## What happens
1. Runs on a timer, and **Already Running?** prevents overlapping runs.
2. **Fetch Find Address Records** takes the records with an incomplete address.
3. **Search Supabase** looks the company up in a reference table of about 95,000
   addresses, using a loose text match to get candidates.
4. **Score & Decide** scores the candidates and picks one only when the match is good
   enough.
5. The record is updated either with the matched address or with a "no match" note, so
   nothing is left in a half-finished state.

## Decisions worth pointing out
- **Postgres, not a spreadsheet.** 95,000 rows searched for every record is not something
  a sheet can do at this pace.
- **A weak match is a "no match".** Filing a plausible but wrong address is worse than
  filing none, because nobody goes back to check the ones that look complete.

## What is in this folder

`workflow.json` is a cleaned copy of the live workflow. Every step, every connection and
every setting is real. The code inside the steps is replaced by a note, and the comments
above each step are kept, because those explain the thinking. Logins, keys, web addresses,
sheet and database IDs, client names and real job links are removed.
