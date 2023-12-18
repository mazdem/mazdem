import random

def generate_code():
    """Generate a random 4-digit code."""
    return [random.randint(1, 6) for _ in range(4)]

def evaluate_guess(secret_code, guess):
    """Evaluate the guess and provide feedback."""
    exact_matches = sum(s == g for s, g in zip(secret_code, guess))
    color_matches = sum(min(secret_code.count(c), guess.count(c)) for c in set(guess)) - exact_matches
    return exact_matches, color_matches

def print_board(turn, guess, feedback):
    """Print the game board."""
    print(f"Turn {turn}: {guess}  Feedback: {feedback}")

def mastermind():
    print("Welcome to Mastermind!")
    print("Try to guess the 4-digit code.")
    print("Each digit is a number between 1 and 6.")

    secret_code = generate_code()
    max_turns = 10

    for turn in range(1, max_turns + 1):
        guess = [int(x) for x in input("Enter your guess (e.g., 1234): ")]
        
        if len(guess) != 4 or any(not 1 <= x <= 6 for x in guess):
            print("Invalid input. Please enter a 4-digit code with digits between 1 and 6.")
            continue

        exact_matches, color_matches = evaluate_guess(secret_code, guess)
        feedback = f"{exact_matches} exact matches, {color_matches} color matches"

        print_board(turn, guess, feedback)

        if exact_matches == 4:
            print(f"Congratulations! You guessed the code in {turn} turns.")
            break

    else:
        print(f"Sorry, you ran out of turns. The correct code was {secret_code}.")

if __name__ == "__main__":
    mastermind()
