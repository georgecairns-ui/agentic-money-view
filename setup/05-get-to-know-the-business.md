# Step 1 of 6: get to know the business

Goal: a short, accurate note in `context/business.md` so what Claude writes for you, from invoice wording to reminders, sounds like it belongs to this business. Ask as little as possible. The next steps go into your money, so keep this one light.

## 1. The first questions

First, follow `setup/first-questions.md`: the talking tip, the first questions (their name, business and website, their computer, Claude plan, where their files are, what they already use, and their goal), then look for what you need yourself and show them what you found. Then ask the questions below, leaving out everything that already answered.

## 2. Ask, in one message

Start from what you found and they confirmed in `setup/first-questions.md` (section 3), and their goal in `context/goal.md`: don't ask for any of it again. Their name, business and website are already in `context/business.md` from `setup/first-questions.md`. Say why in one line, then ask up to 2 questions, leaving out any that's already answered:

> So your invoices and reminders sound like you, a couple of quick questions. What does the business do, and for whom? And what do you spend most of your week on?

## 3. If they gave a website

If you can read web pages, read it first and work out what the business does and who for. Then offer your draft back to them rather than asking again:

> From your website, it looks like [draft]. Is that right, or would you put it differently?

## 4. Fill in the notes

- `context/business.md`: what the business does, who for, and anything else they mentioned (their name, business and website are already there; don't ask for them again). Change its status line to `Status: filled in on <date>`.
- `apps/money/data/money.json`: `settings.businessName` and `settings.ownerName` (their first name).

## 5. Make the app look like their business

Follow `.claude/skills/match-my-brand`: ask for their brand guidelines or website, or 3 quick questions if they have neither, then put their colour, font and logo on the app. If they gave you their website in step 1, say so and offer to use it, so they only have to say yes. Show them the result in light and dark before moving on. If they'd rather keep the standard look, that's fine: skip it.

Tick this step in `setup/progress.md`.
