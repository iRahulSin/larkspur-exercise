# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: We fixed run_agent's tool loop, removed a duplicate tool registration, and wired the MCP server's tools in alongside the original nine — so Claude sees 11 tools total, each with exactly one owner. 

Does: For a customer whose flight got cancelled, it looks up the booking, checks the real flight status, resolves what they're owed under policy, and explains their options in plain language — stopping short of finalizing anything on its own.

Number: Made the process about ~177x cheaper.

Guardrail: The agent never attempted to finalize a rebooking or issue a voucher without the customer choosing a path first. In this trace it made exactly 3 tool calls (lookup, status check, policy check) and stopped at presenting options — proof the "no auto-confirm" rule held on a real case, not just in the schema text.

Next: Fix next_available_day so it accounts for party size instead of answering for one passenger regardless of booking size

Still broken: next_available_day ignores how many people are in the party — a known, documented gap, and this trace doesn't tell us how often it'd matter in practice, since it never got called.

Lever: cost

## Priya asked

Costs: ≈$0.039 per resolved contact (Sonnet 5, this trace: 15,977 in / 683 out tokens) vs. $6.90 for a human contact — about ~177x cheaper.

Wrong: Most likely check_policy gets fed a cause_code/status Claude infers instead of relaying exactly what get_flight_status returned. Nothing downstream checks that they match, so a wrong cause code becomes a wrong policy decision the customer is told as fact.

Runs it: It would still be run by the same customer service reps just the rebooking scenarios would be handled by the agents so that the customers don't have to wait for 40 minutes.

Left out: Party-size handling in next_available_day()
