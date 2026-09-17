# Link Collector

Visits every company careers page on the list and collects the job links, keeping
only the postings in the states the client hires in.

## How it runs
A button in the control sheet, or a timer. Both start the same run.

## What happens
1. **Fetch Companies** reads the list of companies to visit from the control sheet.
2. **Prep Companies** works out how each one has to be fetched. Nearly 40 kinds of
   careers site are handled, and a few careers pages are redirected to the real job
   board behind them.
3. **Loop (rate limit)** goes company by company rather than all at once, so no site is
   hammered.
4. Three fetching routes, cheapest first: a plain web request, then the site's own job
   API where it has one, then a paid rendering service for pages that only exist after
   JavaScript runs.
5. **Extract Job Links** pulls the job links out of the page, and the state filter drops
   postings outside the hiring states.
6. **Append Links** writes the new links into the sheet, **Update Progress** shows the
   count next to that company as it goes, and **Sync Airtable Status** keeps the
   company's record in step.
7. **Notify** posts the day's total to Slack. Companies that returned nothing, or errored,
   are reported instead of passing silently.

## Decisions worth pointing out
- **Try the free route first.** A paid fetch only happens for the page that actually
  needed it, and a site that fails is remembered for seven days rather than forever, so a
  site that fixes itself goes back to the cheap route by itself.
- **A link is copied exactly as the site wrote it**, query string and all, because that is
  what a person copying the link by hand would get.
- **Empty is not automatically fine.** A board that returns nothing gets reported, since
  "no jobs today" and "the page changed and we no longer read it" look identical
  otherwise.

## What is in this folder

`workflow.json` is a cleaned copy of the live workflow. Every step, every connection and
every setting is real. The code inside the steps is replaced by a note, and the comments
above each step are kept, because those explain the thinking. Logins, keys, web addresses,
sheet and database IDs, client names and real job links are removed.
