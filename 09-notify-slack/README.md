# Notify Slack (relay)

One small workflow owns the wording of the messages the system sends. Everything else
sends it numbers.

## Why it is separate
Two different workflows report the day's results, and the messages have to read alike.
Keeping the wording in one place means a change happens once, and the workflows that
report stay as they are: one extra step on a branch, nothing more.

## What is in this folder

`workflow.json` is a cleaned copy of the live workflow. Every step, every connection and
every setting is real. The code inside the steps is replaced by a note, and the comments
above each step are kept, because those explain the thinking. Logins, keys, web addresses,
sheet and database IDs, client names and real job links are removed.
