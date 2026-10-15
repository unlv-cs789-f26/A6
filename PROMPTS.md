# Building with an AI assistant in the browser — prompt guide (A4–A6)

As in A4 and A5 you write the pipelines **with an AI assistant**, not by hand. Measuring and thinking stay
yours: the harness (`soc6`) scores everything the same way for everyone, and the ✍️ questions need your own
reading of your own numbers. Some steps are deliberately manual: the ontology (Part A), the system prompt (C.2),
your handover note (B.3), and the SQL queries (D.3).

## 1. Pick one assistant

| assistant | where | can it type into Colab cells and run them? | notes |
|---|---|---|---|
| **Claude in Chrome** | Chrome Web Store → "Claude" by Anthropic → *Add to Chrome* → pin → click the icon (side panel) | **yes**: it reads the page, clicks, types and runs cells | allow it on `colab.research.google.com` when asked; keep "ask before acting" on for anything else |
| **Gemini in Chrome** | the Gemini button at the top right of Chrome, signed in with a personal Google account | it reads the page and answers in the side panel; you paste the code | good at explaining an error that is on screen |
| **Gemini in Colab** | the ✦ button at the bottom of the notebook, or "Generate" in an empty cell | **yes**: writes into the cell, and its agent mode can run cells | included with Colab Pro; knows the notebook's variables |

## 2. Anatomy of a prompt that works

Every 🛠️ cell already contains a starting prompt with five parts — copy the pattern when you write your own:

1. **Where you are** — "I am in a Google Colab notebook."
2. **What already exists** — the variables and helpers and their shape ("`H.alert_summary(kg, host=...)` returns a list of lines").
3. **The exact contract** — function name, arguments, return type. The check cells call these names.
4. **Constraints** — the library to use, "use pandas groupby, not a loop", "do not modify `soc6`".
5. **Where the code goes and how to verify it** — "Put it in the empty cell under *C.1*, run it, then run the check cell."

## 3. Prompts for the moments you will get stuck

| situation | prompt |
|---|---|
| a cell raised an error | "The cell under B.3 raised the error shown below it. Explain the cause in one sentence, fix the code in that cell only, and re-run it." |
| a check prints FAIL | "The check under C.1 printed `FAIL Q09 missing: ['vpn']`. Print kg_context for that question and change kg_context so the check passes. Do not change the check." |
| a number looks wrong | "My Part D table shows 0 correct turns for every policy. Print the `rewritten` column and tell me whether the rewrite step or the answer step fails." |
| you do not understand the code | "Explain load_history line by line, and what trim_messages keeps for tokens-300 on a 6-message history." |
| a library API changed | "`SQLChatMessageHistory` has no argument `connection` in the installed version. Check `help(SQLChatMessageHistory)` and adapt." |

## 4. What not to do

* **Do not ask for the whole assignment** ("do Part C"). The assistant will invent numbers and answers.
* **Never paste an API key into a prompt or a code cell.** Keys go in Colab 🔑 Secrets and are read with
  `google.colab.userdata.get(...)`.
* **Do not let the assistant edit `soc6/`** or the provided check cells — your numbers would no longer be
  comparable with anyone else's.
* **Do not accept a number the assistant *tells* you.** Only numbers printed by the harness count.
* **Watch what a browser agent reads.** Claude in Chrome and Gemini read the whole page, including log text your
  notebook prints. Text that tells an AI to do something is an injection aimed at
  your assistant. If your assistant suddenly does something you did not ask, stop it and note it in your report.

## 5. What goes in your report (AI-assistant log)

* the assistant you used;
* three prompts you actually sent: one that worked first time, one that failed, and the follow-up that fixed it;
* one place where the assistant wrote code that *ran* but was *wrong*, and how you found out.
