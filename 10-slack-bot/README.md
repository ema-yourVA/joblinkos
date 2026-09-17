# Slack Bot

Lets the client run things and ask questions from Slack, without opening any of the tools.

## What it does
- **"Final Check"** in the channel starts the final pass over the master list and replies
  to say it started, or that it did not and why.
- **The Link Report** posts the day's collection results, with the full list attached as a
  file.
- **Company questions** like "how many links were fetched today for X" are answered from
  the run data the bot already holds, so the reply is instant.

## Decisions worth pointing out
- **The report only mentions exceptions**: boards that errored, or whose numbers no longer
  match what the client expects for them. The full list is still attached. That turned a
  302-line message into 16 lines.
- **The company name does not have to be spelled correctly.** It is matched loosely
  against the names the collector actually reported.
- **No AI in this one.** It is plain code, because every question it answers has one
  correct answer that can be checked.
- If a file upload is refused, the same list is posted as replies instead, so the answer is
  never lost.

## What is in this folder

`workflow.json` is a cleaned copy of the live workflow. Every step, every connection and
every setting is real. The code inside the steps is replaced by a note, and the comments
above each step are kept, because those explain the thinking. Logins, keys, web addresses,
sheet and database IDs, client names and real job links are removed.
