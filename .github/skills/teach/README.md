# Teach

Teach turns a question into a researched, standalone HTML explainer and keeps related learning in the same evolving guide.

```text
/teach vector databases
/teach add hybrid search to my vector databases guide
```

The skill asks only the context that changes the explanation, researches authoritative sources, and writes `.teach/<topic>.html`. Major concepts become navigable tabs; later related questions normally become new tabs in the existing file.

Teach deliberately does not create a formal course system. It has no quizzes, challenges, flashcards, spaced repetition, completion tracking, analytics, accounts, or learner state. The output is simply a clear end-to-end explanation with examples, tradeoffs, and visible citations.

## Research standard

Official documentation, standards, original research, maintainers, and established institutions take priority. Reputable expert and community material may add intuition or practical context, but an isolated blog is never the sole basis for an important claim. Search popularity is treated as one signal, not proof of accuracy.

Every guide includes citations near supported claims and a source ledger explaining who published each source and why it was selected.

## Output

Each guide is one responsive HTML file with embedded CSS and JavaScript. It includes light and dark themes and uses original inline illustrations wherever visuals improve the explanation. Licensed source imagery may be embedded with attribution; unclear or restricted imagery is never copied. The guide opens directly in a browser without a server or runtime dependency. An embedded manifest and stable section markers allow later `/teach` requests to extend it without discarding existing content.

## Install

```bash
npx skills@latest add AshishSalaskar1/skills --skill teach
```

## License

[MIT](../../LICENSE)
