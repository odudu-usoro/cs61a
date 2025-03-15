Comprehensive Explanation of the Hog Project (Problems 0–4)
This guide summarizes the concepts, problems, and solutions implemented so far in the CS61A Hog project. It’s designed to help you connect the dots between the rules, code structure, and underlying programming principles.

Project Overview
Hog is a dice game where players score points by rolling dice or invoking special rules. The project introduces game mechanics like Sow Sad, Boar Brawl, and Sus Fuss, requiring you to simulate these rules using Python. Key concepts include:

Non-pure functions (stateful dice).

Closures (functions that retain state).

Deterministic testing (using test dice).

Mathematical logic (factors, primes, modular arithmetic).

Problems & Solutions
Problem 0: Understanding Dice Mechanics
Goal: Learn how dice.py simulates fair/test dice.
Key Concepts:

Non-pure functions: Functions that change behavior on repeated calls (e.g., make_test_dice cycles outcomes).

Closures: The make_test_dice function returns a nested function that "remembers" the outcomes and current index.
Why It Matters:

Test dice (make_test_dice) ensure predictable outcomes for debugging.

Problem 1: roll_dice (Sow Sad Rule)
Rule: If any die shows 1, the turn score is 1. Otherwise, sum all dice.
Implementation:

Loop num_rolls times to roll dice.

Track if any outcome is 1 (use a boolean flag).

Return 1 if a 1 is rolled; else return the sum.
Key Insight:

Always call dice() exactly num_rolls times (even if a 1 is rolled early).

Problem 2: boar_brawl (Zero-Dice Rule)
Rule: Rolling zero dice scores 3 × |opponent_tens - player_ones| or 1, whichever is greater.
Implementation:

Extract digits:

Player’s ones digit: player_score % 10.

Opponent’s tens digit: (opponent_score // 10) % 10 (handles scores < 10 by treating tens as 0).

Compute max(3 × absolute_difference, 1).
Key Insight:

Avoid strings/lists—use modular arithmetic to isolate digits.

Problem 3: take_turn (Unify Turn Logic)
Goal: Combine roll_dice and boar_brawl into a single turn function.
Implementation:

python
Copy
def take_turn(num_rolls, player_score, opponent_score, dice=six_sided):
    if num_rolls == 0:
        return boar_brawl(player_score, opponent_score)
    else:
        return roll_dice(num_rolls, dice)
Key Insight:

Reuse existing functions to avoid code duplication.

Problem 4: Sus Fuss Rule
Rule: If a player’s score has 3 or 4 factors, it jumps to the next prime.
Implementation:

num_factors(n):

Count divisors from 1 to n (loop and check divisibility).

sus_points(score):

Check if num_factors(score) is 3 or 4.

If true, find the next prime using is_prime (provided).

sus_update:

Call take_turn to get turn points.

Update the player’s total score and apply sus_points.

Example:

sus_points(21) → 21 has factors [1, 3, 7, 21] (4 factors → sus).

Next prime after 21 is 23.

Key Insight:

Prime checking: Increment until is_prime returns True.

Key Takeaways
Closures & State:

make_test_dice uses closures to track the current outcome index.

Modular Arithmetic:

Used to isolate digits (e.g., score % 10 for ones place).

Separation of Concerns:

take_turn delegates to roll_dice or boar_brawl, keeping code modular.

Edge Cases:

Always test for scores < 10, zero outcomes, and boundary primes.

How It All Fits Together
take_turn handles the core turn logic (rolling dice or Boar Brawl).

sus_update extends this by applying the Sus Fuss rule to the updated score.

Test dice ensure deterministic behavior, making debugging easier.

Next Steps
Problem 5+: Likely involve additional rules (e.g., swapping scores) or strategies.

Testing: Use ok to verify edge cases and refine logic.

By understanding these foundational concepts, you’ll be prepared to tackle more complex game mechanics in later phases! 🚀