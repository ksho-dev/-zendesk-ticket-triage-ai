# Zendesk Ticket Triage Prompt

This is the structured prompt that powers the triage assistant. It is designed to be pasted into Claude in Chrome while viewing the Zendesk ticket queue.

## Full Prompt

```
You are helping me triage my Zendesk ticket queue. Look at all open and pending tickets assigned to [AGENT NAME] and organize them for me. Follow these rules:

1. EXCLUDE tickets created today or yesterday from the main list — put these at the very bottom under a section called "TODAY & YESTERDAY".

2. For all other tickets, identify the ones I have NOT responded to yet.

3. Read the conversation of each unanswered ticket and flag it as URGENT if:
   - The customer used urgent language (urgent, ASAP, emergency, still waiting, this is unacceptable, etc.)
   - There is a pending escalation that was never followed up
   - The customer has written more than once without getting a response

4. Organize the final list in this exact order:
   - URGENT tickets first (oldest to newest)
   - Then tickets I have not answered in more than 48 hours (oldest to newest)
   - Then the rest of the unanswered tickets (oldest to newest)
   - Finally, the TODAY & YESTERDAY section at the bottom

5. For each ticket show me: ticket number, customer name, how many hours/days without a response, and one short sentence describing what the customer needs.

Start now and give me the organized list.
```

## Design Notes

**Why exclude today/yesterday?**
Tickets that just arrived haven't been waiting long, so they shouldn't compete for attention with customers who have been waiting days. Pushing them to the bottom keeps focus on genuine backlog.

**Why read the conversation instead of just sorting by date?**
Date alone misses urgency. A customer who wrote "still waiting, this is urgent" three times deserves priority over an older but calm ticket. Reading content lets the assistant catch what metadata can't.

**Why a fixed output format?**
A scannable, consistent format (number, customer, wait time, summary) makes the result immediately actionable instead of requiring me to re-read everything.
