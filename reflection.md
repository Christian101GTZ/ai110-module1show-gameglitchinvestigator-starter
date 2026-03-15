# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it? 
When I first ran the game I input a number and nothing worked and no loading at all. It was inconsistent. When I tried restarting the game it was less consistent as well  it was not restarting. It was not working consistently as a normal website should.

- List at least two concrete bugs you noticed at the start  
So when I played around with the game I entered 1 and it said to go lower, and then when I entered 0 it told me to go lower. Which is weird since the game states to guess between 1 to 100, meaning you can't go lower than one. Another thing is when I failed the game it said the secret number was 7 even though I was entering numbers from 80 and above and it was telling me to go higher and then lower until I reached the limited amount.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)? So the tool that I primarily used was Claude since Codepath provided us with access to it.
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
Claude helped me identify a bug on lines 158-161 where a number was being converted to a string on even attempts. Once I asked Claude to help me explain what was happening with a simple analogy, I then applied the fix to the problem.

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
Something that happened was that Claude gave me all 7 bugs at once without telling me which to fix first. This was overwhelming and made it hard to focus on one problem at a time. It only became helpful once I asked it to explain a specific bug step by step. I learned that breaking things down is important to not feel overwhelmed and to efficiently fix an error. Another thing is that Claude added extra code inside check_guess to handle a string comparison error, but that bug was already fixed elsewhere. I verified it was unnecessary by checking app.py where the fix was already applied. 

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

Claude helped me understand what to look for when testing. By explaining that the bug only triggered on even attempts, I knew to specifically test my guess on attempt 2 and attempt 4 to confirm the fix worked.

For Bug 1 (hint direction), I ran pytest on tests/test_game_logic.py with 5 tests targeting check_guess. The tests verified that a guess of 80 against a secret of 50 returns "Too High" with a "Go LOWER" message, and a guess of 20 returns "Too Low" with a "Go HIGHER" message. All 5 tests passed after the fix was applied. Claude helped design the tests by explaining the expected output for each case so I knew exactly what to assert in the test.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number? 

The secret number kept changing because of how the whole page basically reruns from top to bottom. So that meant that random.randint() was called fresh every rerun, giving a new secret each time. Every button click meant that the whole page runs again from top to bottom — it basically rewinds from the beginning every time you press.
Session state is like a backpack that the game carries between reruns. Anything that I put in the backpack survives the rerun, and it is vital since without it everything gets dropped on the floor.
I was able to fix it by adding a check that says only to pick a new secret if there isn't one already in the backpack. So the first run picks the number, puts it in the backpack, and every run after uses the same one.


---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
I think that the most important lesson I learned from this lab is to break everything into pieces in order to work on fixing the problem more effectively. It is also important to use AI to help explain what the problem is in a simplified way so I don't feel overwhelmed with the information.
One thing that I would do differently next time would be to ask AI to explain its suggestions when fixing a problem, since many times it might add unnecessary things to the code and it is important to ask why.
I learned that AI can obviously write code fast but many times it lacks context, so it might not always be right or necessary. It is important to read the code and understand what changes to make before just accepting its suggestions. 
