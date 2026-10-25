# magic-8-ball

A Magic 8 Ball webpage. Type a yes-or-no question, shake the ball, and an answer floats up in the window.

## What it does

- **Classic answers**: the 20 answers from the original toy (10 yes, 5 maybe, 5 no).
- **Bonus answers**: 10 extra faces that aren't on the real die, such as "Signs point to pizza." and "Ask Ellie."
- **Shared custom answers**: anyone with edit access can add their own answers. Each one is saved to a shared database, so everyone who opens the page can get it on a shake. You can remove answers you added. The page owner can remove any added answer.
- **Random picks**: each shake draws from every face (classic, bonus and added) using the browser's cryptographic random number generator. It never gives the same answer twice in a row. If you ask the exact same question twice in a row, the ball sometimes calls you out on it.
- **Secret rule**: a question that ends in two question marks (like `Should I??`) always gets "Ask Ellie."
- **Recent shakes**: your last six questions and answers for the current visit. Only you see them, and they aren't saved.

## How it's hosted

`index.html` is the source of a private page hosted on claude.ai. claude.ai provides the shared database through `window.claude.use("db")`, so there's no server to run.

GitHub Pages wasn't used because Pages sites are always public and can't store shared data.

### Who can use it

The page is private to its owner until it is shared from the page's **Share** menu on claude.ai:

- To let someone shake the ball **and add answers**, invite them by email as an **Editor**. Leave public link sharing off, because a public link stops outside editors from saving answers.
- Viewers can shake and see every answer, but can't add answers.
- Everyone needs to be signed in to claude.ai to see the shared answers.

If you open `index.html` straight from this repo, the ball still works with the classic and bonus answers. The shared answers only load on the hosted page.

## Data

Added answers are stored in the `answers` collection, one document each:

```json
{ "text": "Only after coffee.", "tone": "yes", "addedBy": "<opaque user id>", "createdAt": 1792043900000 }
```

`tone` is one of `yes`, `maybe` or `no`, and decides which column the answer appears in. Answers are limited to 60 characters so they fit on the die.

## Changing the built-in answers

Edit the `CLASSIC` and `BONUS` lists near the top of the `<script>` in `index.html`, then republish the page.
