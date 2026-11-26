# Step 2 of 6: your accounts software (required)

Goal: Claude can read the person's accounts software through a live connection, proven with a real read and recorded. **Agentic Money View works on top of an accounts app, and it can't work without one, so this step is required.** Supported today: **Xero** (fully) and **QuickBooks** (only when the person's Claude shows Intuit's QuickBooks connector, which Intuit says is for US customers only for now; whether it opens to UK customers: to check). FreeAgent, Sage and any other accounts app have no Claude connector, so they are **not supported yet**.

The tools named in this step are often not loaded yet: search your tools for them first.

## What the connections can really do

Say these plainly, once, when they matter. Don't promise more.

- **Xero:** the Xero connection in the Claude app **reads only**: invoices, bills, bank transactions, contacts, cash position and what customers owe. It can't create an invoice. Money View opens Xero's new invoice page for them to raise it there.
- **QuickBooks:** Intuit's connector reads invoices, payments and bank transactions, and can also create invoices. Claude only ever creates one when the person presses the button, and never sends it.
- Whatever the app, Claude never sends, approves or deletes an invoice, and never moves money. Money View builds the money view only through a live connection, never from exports, spreadsheets or reports.
- Where a connection guide says Claude may create, update or send something when asked, Money View's rule wins: Claude never sends, updates or deletes an invoice or estimate and never creates a payment link. It creates an invoice only as a draft, only after the person presses 'Put it in <app> as a draft'.

## 1. Which accounts software

If `setup/first-questions.md` already told you (what they already use), say what you found rather than asking again. Otherwise ask: **"Which accounts software do you use?"** Xero, QuickBooks, something else, or none. Don't suggest one yet. Check `context/tools.md` and `apps/home/data/connections.json` too: if their accounts app is already recorded there, say so and check it in part 2 rather than starting again.

## 2. Connect it and prove it

Follow the guide for their app and `.claude/skills/connect-a-tool`: find the route, look up this session's connections (`session_connectors_status`), then switch it on, reconnect it or point them to Connect, by the table in `connect-a-tool` ("Check, switch on, or point to Connect"). Never ask what's on their screen: you can see the status yourself. Keep going round until it's on. Say "a connection", never MCP, API, JSON or repo.

- **Xero:** `setup/connections/xero.md`.
- **QuickBooks:** `setup/connections/quickbooks.md`. Use only Intuit's own "Intuit QuickBooks" connector. If they aren't a US QuickBooks customer, or Claude doesn't show it, there's no Claude connector for them: go to part 3.

**Prove it** with one harmless read, with their permission: list their unpaid invoices and say, with their real figures, "I can see 4 unpaid invoices, the oldest from 12 September." Then read their latest invoice for its number (for the default prefix below). Only after a read works, record it (part 4).

Then look at the tools the connection offers and set `sources.accounts.mode`: `drafts` if it can create invoices (QuickBooks through Intuit's connector, or for Xero only the optional drafts connection if it is already there), otherwise `read`. Don't offer the Xero drafts connection here: it is an optional extra for later, and the hand-over says how to ask for it.

## 3. If there's no connector, or no accounts software

- **FreeAgent, Sage, QuickBooks outside the US, or anything else:** follow its guide in `setup/connections/` if there is one (`freeagent.md`, `sage.md`, `quickbooks.md`); for any other app, search Claude's connector directory (`search_mcp_registry`) as `connect-a-tool` says. If a connector from the app's maker turns up, tell them Money View hasn't been checked with it yet and stop as below. With no connector, say this sentence, word for word with the app's name:

  > There's no Claude connector for [app], so I can't connect to it live. If you export a CSV or PDF from it and drop it in the files folder, I'll read it whenever you ask.

  Record it as `export-only` (part 4). Here the shared guides' steps that ask for an export (and any 'Prove it' that reads one) do not apply: after the sentence and the record, don't ask for an export, don't read one to prove anything, and don't build anything from one. If they bring one anyway, read it in chat only when they ask, as a snapshot, and never write it into the money view. Then say, in one plain paragraph:

  > Money View itself needs a live connection to your accounts app to build your money view, so it can't work from your accounts app yet. It works with Xero today, and QuickBooks will work once Intuit's Claude connection reaches the UK. Once your accounts app is one of those, come back and type /setup and we'll pick up from here.

  Then give the one-line book-a-call offer from `.claude/skills/connect-a-tool` (part 4), once, with what the app does for them in the row's `note`.

  Leave this step unticked, put "Waiting for a supported accounts app" in `setup/progress.md` and stop. Setup doesn't go on to the bank or the rest without a live connection.

- **None** (Word, Excel, a notebook): stop politely, in one plain paragraph:

  > Money View works on top of your accounts software, so it can see your invoices and your bank. Without one, there's nothing for it to read. I'd talk to your accountant about which one suits you. It works with Xero today, and QuickBooks will work once Intuit's Claude connection reaches the UK. Once you've got one, come back and type /setup and we'll pick up from here.

  Leave this step unticked, put "Waiting for an accounts app" in `setup/progress.md` and stop.

## 4. Record it

- `apps/home/data/connections.json` (format in `setup/connections/README.md`, "Recording a connection"): create it if it isn't there, as `{ "version": 1, "connections": {} }`. Add the accounts app's row with the key and wording its guide gives: `connected` with today's date in `checked` only after the read in part 2 worked; `export-only` (or `no-connector` if they don't want to export) for an app with no connector.
- `context/tools.md`: the connection, as its guide says.

For QuickBooks, in context/tools.md and the note, write the never-list as: 'Send, update or delete an invoice or estimate, create a payment link. Create an invoice only as a draft when they press Put it in QuickBooks as a draft.'

## 5. If it still won't connect

If Xero or Intuit's QuickBooks connector is there but still won't connect after the loop in `connect-a-tool`, say what went wrong in one plain line and record the row as `needs-attention`, with what went wrong in `note`. The Connections box on Home shows a **Fix it** button for it. Money View can't build anything without this connection, so leave this step unticked, put "Accounts connection needs attention" in `setup/progress.md`, tell them they can press **Fix it** on Home or type /setup to try again, and stop here. Never ask for a password or a key in chat.

## 6. If it's waiting on someone else

If the connector needs their Claude Owner to add it, or their IT administrator to approve it (on a Team or Enterprise plan, `setup/connections/where-to-click.md`), park it (`.claude/skills/connect-a-tool`, "Waiting on someone else"): offer to draft the short message they can send, record the row as `waiting` with `waitingOn` (who, such as "IT") and the one thing still to do in `note`, and add "Accounts connection waiting on <who>" to "Notes for next time" in `setup/progress.md`. Leave `sources.accounts.mode` as `none`. Say plainly, in one line: "Your money view fills in once your accounts app is connected. When it is, press Finish connecting on Home, or tell me." Ask about payment terms (part 7), tick this step with the note "accounts app waiting on <who>", and go on to step 3 (`setup/money-02-your-bank.md`).

When it's finished later (Finish connecting, or they tell you), `connect-a-tool` part 2a proves it with a read and then does what setup would have done with it. For the accounts app that is: part 8 of this step (`sources.accounts`, the invoice prefix), the bank feed check in `setup/money-02-your-bank.md` (questions 2 and 3), then `.claude/skills/update-my-money-view` and confirming the regular payments it suggests (`setup/money-03-money-out.md`, parts 1 and 2), so the money view fills in.

## 7. Payment terms

Once the connection is proven, ask: **"How many days do you usually give people to pay?"** Save as `settings.invoice.termsDays` (30 if they don't know). Mention that the invoice numbers come from their accounts software, so you don't ask about those.

## 8. Save as you go

- `apps/money/data/money.json`: `sources.accounts` (`app`, `mode`, `checkedAt` now), `settings.invoice.termsDays` and `settings.invoice.prefix` (from their latest invoice number, as a default only).
- `context/money.md`: under "Accounts app and how we invoice", what they use, how invoices are sent, and the terms, in their words. Change its status line to `Status: filled in on <date>`.

## 9. What else they already use

For anything else they said they already use for this side of the business (`setup/first-questions.md`: a cash flow spreadsheet, their own dashboards, a CRM), follow `.claude/skills/connect-a-tool`. It doesn't feed the money view, so say so in one line. One with a connector is connected and proven only if they'd like it. One with no connector gets the shared no-connector sentence from part 3 (only the sentence: part 3's stop is for the accounts app), is recorded as `export-only` with what it does for them in `note`, and gets the one-line book-a-call offer from `.claude/skills/connect-a-tool` (part 4), once. One waiting on someone else is parked as `waiting`.

Tick this step in `setup/progress.md`.
