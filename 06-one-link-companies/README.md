# One Link Companies

Some careers pages list every opening on a single page, with no separate link per job.
The normal collector has nothing to follow, so those companies are handled here.

## What happens
1. **Fetch Companies** picks the companies flagged for this route in the control sheet,
   so the client can add or remove one without any code change.
2. **Seed Queue** writes the company names into the sheet immediately, so the run shows
   what it is doing from the start instead of staying blank.
3. The page is fetched, cheapest route first, same as everywhere else.
4. **Split Postings** asks the model only for the list of job titles.
5. **Collect Company** then cuts the posting bodies out of the page text in code, from one
   title to the next, so every description is the page's own words and never the model's
   paraphrase.
6. **Check the master list** and **Decide Write** work out which postings are genuinely new.
7. New postings are filed, counts are written back per company, and problems go to Slack.

## Decisions worth pointing out
- **The model is used for the cheap part only.** Titles are short and verbatim; bodies are
  sliced out by position in the page text.
- **"Already submitted" means title, salary and description all match.** If the pay changed
  or the description was rewritten, it is treated as a different job and entered.
- **The address is resolved once per company**, because these pages rarely repeat the
  office address inside each posting.

## What is in this folder

`workflow.json` is a cleaned copy of the live workflow. Every step, every connection and
every setting is real. The code inside the steps is replaced by a note, and the comments
above each step are kept, because those explain the thinking. Logins, keys, web addresses,
sheet and database IDs, client names and real job links are removed.
