# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").


When I first ran the game, it looked normal, but it didn't work correctly. Pressing Enter did nothing, so I had to click "Submit Guess". The hints were backwards: when I guessed 1 (the lowest number) it told me "Go LOWER", and when I guessed 99 and the secret was 90 it told me "Go HIGHER". I also ran out of attempts one guess early, and the "New Game" button didn't start a new game after I lost.

**Bug Reproduction Log**

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| Guessed 1 | "Go HIGHER" (1 is the lowest number) | "Go LOWER" | No error |
| Guessed 99 (secret was 90) | "Go LOWER" | "Go HIGHER" | No error |
| Played on Normal (8 attempts allowed) | 8 attempts | Game ended after 7 attempts | No error |
| Clicked "New Game" after losing | A new game starts | Stuck on "Game over. Start a new game to try again." | No error |
| Guessed 100 on my 2nd attempt (after fixing the hints) | "Go LOWER" | "Go HIGHER" (on every even attempt the secret was turned into text, so the comparison broke) | No error |
| Made my first guess on Normal | "Attempts left" goes from 8 to 7 | Still showed 8, so the counter was always one behind and I thought I had one more guess left | No error |
| Lost the game, then clicked Submit again | Still see what the secret number was | The "The secret was..." message disappeared and only "Game over" was shown | No error |


---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
