# CodeAlpha_Hangman-Game
import random

# List of words to guess from
word_list = ["apple", "chair", "zebra", "snake", "grape"]

# Randomly select one word
selected_word = random.choice(word_list)

# Uncomment the line below only if you want to test the selected word
# print("The word is:", selected_word)

# To keep track of correct guesses
guessed_letters = []
chances = 6

print("Hangman Game - Created by Tarun")
print("You have 6 chances to guess the correct word.\n")

# Main game loop
while True:
    current_state = ""
    for ch in selected_word:
        if ch in guessed_letters:
            current_state += ch + " "
        else:
            current_state += "_ "
    print("Word:", current_state.strip())

    # Win check
    if all(letter in guessed_letters for letter in selected_word):
        print("\nYou guessed it right! The word was:", selected_word)
        break

    # Take input from user
    user_input = input("Enter a letter: ").lower()

    # Check for valid input
    if not user_input.isalpha() or len(user_input) != 1:
        print("Enter only a single alphabet letter.")
        continue

    # Check if letter already guessed
    if user_input in guessed_letters:
        print("You already tried that letter.")
        continue

    # Add the guess to the list
    guessed_letters.append(user_input)

    # Check if the guess is correct
    if user_input in selected_word:
        print("Nice! That letter is in the word.")
    else:
        chances -= 1
        print("Wrong guess. Tries left:", chances)

    # Loss check
    if chances == 0:
        print("\nYou lost! The correct word was:", selected_word)
        break
