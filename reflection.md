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

I used Claude (Claude Code in VS Code) as my AI assistant. One correct suggestion: I asked Claude to "move the `check_guess` function to `logic_utils.py`, fix the high/low bug, and update the import in `app.py`." It moved the function, swapped the hint messages so a guess that is too high says "Go LOWER", and added `from logic_utils import check_guess` to `app.py`. I reviewed the diff in the Source Control tab, then played the game and checked that guesses above and below the secret gave the right hints, and the pytest tests passed. One suggestion I did not accept as written: after I found two more small bugs (the "Attempts left" counter is always one behind, and the secret number disappears if you click Submit after losing), Claude offered to fix them too. I decided they were out of scope for now, because the assignment only asks for two fixes and I had already fixed four, so I logged them in my bug table instead. I checked that the game still works fully without those fixes.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I only counted a bug as fixed when I could play the game and see the correct behavior myself, and when pytest passed. Playing again was important: after fixing the hints, I guessed 100 and the game still said "Go HIGHER". That showed me a hidden bug where the secret was turned into text on every even attempt, so "100" was compared to the secret like a word instead of a number. When I first ran `pytest`, all 3 tests failed (`FFF`) because the tests expected `check_guess` to return only `"Win"`, but it returns two values: the outcome and the message. Claude explained the error, and we changed the tests instead of the function, because `app.py` needs the message to show the hint. Claude also helped me add two new tests that check a guess that is too high says "LOWER" and a guess that is too low says "HIGHER". In the end, all 5 tests passed.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

Every time you click a button in a Streamlit app, it runs the whole Python file again from the top. This is called a "rerun". Because of that, normal variables are reset every time. `st.session_state` is like a notebook the app keeps between reruns, so values like the secret number, the attempts, and the game status are saved. I saw this in the "New Game" bug: the button reset the attempts and the secret, but it did not change `status` back to `"playing"` in the session state, so after the rerun the game still thought it was over.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to keep is testing the real app again after every fix, not just trusting the code, because that is how I found the hidden "secret becomes text" bug. I also want to keep committing after each phase so my progress is saved. Next time, I will be more careful when reviewing diffs in VS Code, because I accidentally clicked the revert arrow and undid a fix. I will also check which folder my terminal is in before running commands like `git clone`. This project showed me that AI-generated code can look fine and still have many hidden bugs, so I need to test it and understand it before I trust it.
