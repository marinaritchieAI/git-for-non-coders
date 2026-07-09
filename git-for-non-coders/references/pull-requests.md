# Writing pull requests a non-coder can review

A pull request is the moment the user decides whether a change goes ahead. If they cannot understand it, the review is theatre and the safety it provides is imaginary.

Write the description for someone who will never look at the diff.

## The standard

Every pull request description answers three questions, in this order:

1. **What changed**, in behaviour, not in code.
2. **What will be different** once this is merged.
3. **What to check** before approving, if anything.

Keep it to a short paragraph and a few lines. Never paste the diff into the description.

## Format

```markdown
## What changed
[One or two sentences, describing behaviour. No file names, no function names.]

## What will be different after merging
[Concretely, what the user or their customers will experience.]

## Worth checking
[Anything the user should verify, or "Nothing. This is a small internal change."]
```

## Examples

**Example 1**

Input: added a call to `sharp().resize(1200)` in `upload-handler.js` before the S3 put.

Output:

> ## What changed
> Photos are now resized before they are saved.
>
> ## What will be different after merging
> Uploaded photos will be scaled to 1200 pixels wide. Previously they were stored at their original size, which made pages slow to load.
>
> ## Worth checking
> If you rely on full-resolution originals anywhere, tell me before merging, because those will no longer be kept.

**Example 2**

Input: changed `MAX_RETRIES` from 3 to 5 and added exponential backoff in the email client.

Output:

> ## What changed
> When sending an email fails, the system now tries more times, and waits longer between each try.
>
> ## What will be different after merging
> Fewer emails will be lost when the mail provider is briefly unavailable. A failing email may now take up to a minute to give up, rather than a few seconds.
>
> ## Worth checking
> Nothing. This is a small internal change.

**Example 3, a change with real consequences**

Input: modified the invoice generator to apply GST at 10 percent.

Output:

> ## What changed
> Invoices now add GST at 10 percent.
>
> ## What will be different after merging
> Every invoice generated from now on will show a GST line and a higher total. Invoices already sent are unaffected.
>
> ## Worth checking
> This changes what customers are charged. Please confirm the rate is correct, and that GST should apply to all invoice types, before merging.

## Rules

- **No jargon.** Not "refactored", not "endpoint", not "middleware". If a technical word is unavoidable, define it in the same sentence.
- **Lead with the consequence, not the mechanism.** The user cares that photos get smaller, not that `sharp` was called.
- **Flag anything irreversible or outward-facing.** Money, emails to customers, published content, deleted data. Say so plainly under "Worth checking".
- **One concern per pull request.** If the change touches two unrelated things, open two pull requests. A user cannot approve half a request.
- **Be honest when it is trivial.** "Nothing. This is a small internal change" is a useful thing to say, and it teaches the user where to spend their attention.

## After opening it

Tell the user, in the chat: what the pull request does, the link to it, and exactly what pressing merge will cause to happen. If merging deploys to something live, say that sentence out loud every time. Do not assume they remember from last week.
