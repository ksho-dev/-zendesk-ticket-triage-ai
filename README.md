# AI-Powered Zendesk Ticket Triage Assistant

An AI automation that reads a support agent's Zendesk queue, identifies unanswered tickets, prioritizes them by urgency, and surfaces the ones that need attention first — turning a manual, error-prone daily routine into a fast, consistent process.

## The Problem

As a support agent handling a high volume of tickets, I faced a recurring problem: there was no easy way to see which customers had been waiting the longest without a response. Zendesk showed the date a customer first wrote, but not a clear "oldest unanswered first" view that also flagged urgent cases or forgotten escalations.

This meant:
- Tickets from days ago could sit unanswered while newer ones got attention
- Urgent customer messages were easy to miss in the noise
- Escalations I had already raised but never heard back on would fall through the cracks
- Prioritizing the queue manually took time and was inconsistent

## The Solution

I designed an AI assistant (using Claude in Chrome) that reads the ticket queue and reorganizes it based on real priority logic, not just date. The assistant:

1. **Filters to my tickets only** — processes only tickets assigned to me
2. **Identifies unanswered tickets** — separates what actually needs a response from what's already handled
3. **Sorts oldest-to-newest by wait time** — so the customer who has been waiting longest comes first
4. **Flags HIGH PRIORITY cases** by reading each conversation and detecting:
   - Urgent language from the customer (urgent, ASAP, still waiting, etc.)
   - Escalations that were raised but never followed up
   - Customers who wrote more than once without a reply
5. **Pushes today's and yesterday's tickets to the bottom** — since those haven't been waiting long
6. **Returns a clear action list** — ticket number, customer, hours waiting, and a one-line summary of what they need

## Impact

- Turned a manual prioritization routine into an automated, repeatable process
- Reduced the risk of long-waiting customers being overlooked
- Made urgent cases and forgotten escalations visible instead of buried
- Brought consistency to how the queue was triaged every day

## How It Works (Prompt Design)

The core of this project is the prompt engineering. The assistant is driven by a structured prompt that defines clear rules and priority order. Key design decisions:

- **Explicit exclusion rules** (today/yesterday to the bottom) to focus attention on genuinely waiting tickets
- **Conditional flagging logic** so the AI reads conversation content, not just metadata, to detect urgency
- **A fixed output format** (ticket number, customer, wait time, summary) so the result is scannable and actionable

See [`prompt.md`](prompt.md) for the full prompt.

## Tools Used

- Claude (via Claude in Chrome) for reading and reasoning over the queue
- Zendesk as the support platform
- Prompt engineering to encode the prioritization logic

## What I Learned

- How to translate a fuzzy human judgment ("which ticket matters most right now") into explicit, repeatable rules an AI can follow
- That the hardest part of automation isn't the tool — it's defining the logic clearly enough that the output is trustworthy
- How small changes in prompt wording (e.g. defining what counts as "urgent") significantly change output quality

---

*This project is based on a real workflow I built and used in a support role. Ticket details and customer information are not included for privacy reasons.*
