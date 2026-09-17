# Main Filter

Decides which of the collected links are genuinely new, and files the new ones.

## What happens
1. **Fetch Unfiltered Rows** takes the rows that have no status yet.
2. **Plan Chunks** splits them into batches, because the whole list at once is too much
   for one request.
3. **Check master list** asks the master database, once per batch, whether it already
   holds each link.
4. **Decide Statuses** marks each row: already there, or new.
5. **Salary Gate** drops postings that obviously pay too little before anything more
   expensive happens to them.
6. **Push New** files the new ones, **Write Statuses** writes every row's result back to
   the sheet, and **Notify** reports when a batch, a write or a push fails.

## Decisions worth pointing out
- **One search per batch, not one per link.** The same check done row by row was the
  slowest part of the day.
- **Matching is substring-based**, on purpose: it copies how the master list itself
  stores and compares links, so the result matches what a person checking by hand would
  get.
- **Every failure has its own message.** A batch that fails, a write that fails and a
  push that fails are three different problems, and saying which one happened is the
  difference between a five-minute fix and an afternoon.

## What is in this folder

`workflow.json` is a cleaned copy of the live workflow. Every step, every connection and
every setting is real. The code inside the steps is replaced by a note, and the comments
above each step are kept, because those explain the thinking. Logins, keys, web addresses,
sheet and database IDs, client names and real job links are removed.
