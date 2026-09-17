# Data Scraper

Opens each new posting, reads it with an AI model, and files a complete record.

## What happens
1. **Fetch Unprocessed Records** takes the postings waiting to be read.
2. **Already Running?** stops a second run starting on top of the first.
3. The page is fetched by the cheapest route that works: plain request, then a reading
   service, then a paid rendering service.
4. **Content OK?** checks what came back is really a page: proper structure, enough real
   text, and none of the wording a "prove you are not a robot" page uses.
5. **Low Pay Scan** drops obviously underpaid postings before the model is called, so
   they cost nothing.
6. **Build Prompt** and **Openrouter API** read the posting field by field.
7. **Parse & Normalise** checks the model's answer against rules in ordinary code, and
   corrects it where the rules are clear.
8. Anything that cannot be read is filed with the reason, not dropped.

## Decisions worth pointing out
- **The model reads. Code decides.** Pay thresholds, state filters, duplicate checks and
  counting are all ordinary code, because those have to be right every single time.
- **A page full of content can still be a failure.** The worst pages here were never blank;
  they were robot checks that looked perfectly normal.
- **A bad answer is never saved as blank.** An empty value matches no filter and the
  record silently disappears. A wrong value is visible and gets caught.

## What is in this folder

`workflow.json` is a cleaned copy of the live workflow. Every step, every connection and
every setting is real. The code inside the steps is replaced by a note, and the comments
above each step are kept, because those explain the thinking. Logins, keys, web addresses,
sheet and database IDs, client names and real job links are removed.
