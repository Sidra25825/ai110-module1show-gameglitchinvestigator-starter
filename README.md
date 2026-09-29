# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] **Describe the game's purpose.** It's a number guessing game built with Streamlit. The game picks a secret number, the player guesses, and hints say whether to go higher or lower until the player wins or runs out of attempts.
- [x] **Detail which bugs you found.**
  - The hints were backwards (a guess that was too high said "Go HIGHER").
  - The secret was turned into text on every even attempt, so comparisons like "100" vs "57" gave wrong hints.
  - Attempts started at 1 instead of 0, so the player lost one attempt.
  - "New Game" did not reset the game status, so the game stayed stuck on "Game over".
  - Not fixed yet (logged in `reflection.md`): the "Attempts left" counter is one behind, and the secret disappears if you click Submit after losing.
- [x] **Explain what fixes you applied.**
  - Moved `check_guess` into `logic_utils.py`, swapped the hint messages, and imported it in `app.py`.
  - Removed the code that turned the secret into a string, so it always stays a number.
  - Changed the starting value of `attempts` from 1 to 0.
  - Made "New Game" reset `status` to `"playing"` and clear `history`.
  - Updated the tests to match `check_guess`'s `(outcome, message)` return value, and added 2 new tests for the hint messages.

## 📸 Demo Walkthrough

Describe your fixed game in numbered steps so a reader can follow along without watching a video:

1. The player opens the game on Normal difficulty (range 1 to 100, 8 attempts). For this example, the secret is 51.
2. The player guesses 50, and the game says "📈 Go HIGHER!"
3. The player guesses 52, and the game says "📉 Go LOWER!"
4. The player guesses 51, and the game says "🎉 Correct!" and shows the secret and the final score.
5. The player clicks "New Game", and a fresh game starts with a new secret number.

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

```
$ python -m pytest tests/
tests\test_game_logic.py .....                                           [100%]
============================== 5 passed in 0.02s ==============================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
