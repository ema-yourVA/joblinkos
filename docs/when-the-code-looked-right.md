# When the code looked right and wasn't

**What this system does, in two sentences:** it visits hundreds of company careers pages,
collects the job postings, has an AI read each one, and files the details into a database.
Work that used to be done by hand, all day, every day.

Almost all of it was built with Claude, and I still use Claude for a weekly check of the
live system. So my real job here is not typing the code. It is deciding whether the result
is actually right.

Here are four times it was not, even though everything looked fine.

---

## 1. A small number that was not a small number

A company's careers page kept giving us 16 jobs. That looked normal. Small company, few
openings, nothing to ask about.

They actually had 557.

Two things were hiding them. Their website makes visitors pass a "prove you are not a
robot" check, which makes every page load slowly, so our run ran out of time long before it
reached the end of the list. And their list only said "Multiple locations", while the real
city and state sat further down inside each job.

So I opened their site myself and watched what their own page does when you use its
filters. It sends a short code to their server. Now we send that same code, and their site
hands back only the jobs we want. 557 jobs, in under three minutes.

**The lesson:** a wrong answer usually looks like a perfectly normal answer. Sixteen looked
like a small company. It was a mistake wearing a small company's clothes.

---

## 2. The number I was given, against the number I could prove

Another board reported 59 jobs, and that is what we collected. My client looked at it and
said it should be closer to a thousand.

She was right. Their page shows 10 jobs at a time, not 20, and the code had been written
assuming 20. So it worked out how many pages to visit, got that number wrong, walked half
the board, and stopped. The run finished normally and reported no problem at all.

A full walk of every page found 1,020 jobs.

Since then, before any new site goes live, I check what we collect against a number the
site itself publishes. If their page says 1,620 openings, we have to return 1,620, not
"roughly that".

**The lesson:** the numbers worth checking are the ones nobody has any reason to doubt.

---

## 3. Paying every day for something that never changes

Some pages need a paid service to read them. The bill was about $19 a month, and one
company alone was about $11.50 of it.

Why: we opened all 383 of that company's job pages every single day, just to read the
office address off each one. Addresses do not change. And the next step of the system was
throwing nearly all of those jobs away anyway, because it had already seen them yesterday.

Now we only re-open a page when the site's own index says that page was updated. On a day
with nothing new, we pay for nothing at all, and the result is identical. With the rest of
that review, the running cost of the whole system came down 42%, and it still does
everything it did before.

**The lesson:** the expensive part is rarely the part that looks expensive. It is the small
thing you pay for every day without asking whether anything changed.

---

## 4. Nothing broke, and almost every AI call was wrong

The AI is asked to return its answer as clean, structured data, so the rest of the system
can file it automatically.

We reach the AI through a service that picks whichever provider is cheapest at that moment.
When I pulled a month of records, about 97 out of every 100 calls had gone to a provider
that cannot follow that instruction.

Nothing failed. The answers simply came back as ordinary sentences instead, and the next
step did its best with them. It only came to light because I read the bill.

The fix was to say which providers are allowed and to require that they support the
setting. While I was there, I also moved to a cheaper model of similar quality: about $50 a
month became about $15, for the same work.

**The lesson:** AI sounds exactly as confident when it is wrong as when it is right. So I
never give it a job whose answer I cannot check afterwards.

---

## What ties these together

A loud failure is easy. Somebody sees it and it gets fixed. The dangerous ones are the runs
that finish, report success, and quietly hold the wrong answer.

So in this system: anything that fails has to say so out loud, in Slack. And anything that
saves has to be checked against a number a person can verify.
