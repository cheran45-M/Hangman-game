# Hangman-game
import random

# Predefined list of words
word_list = ["apple", "house", "robot", "pizza", "snake"]

# Randomly select a word
secret_word = random.choice(word_list)
guessed_letters = []
incorrect_guesses = 0
max_attempts = 6

# Create a display version of the word with underscores
display_word = ["_"] * len(secret_word)

print("🎮 Welcome to Hangman!")
print("Guess the word, one letter at a time.")
print(f"You have {max_attempts} incorrect guesses allowed.\n")

while incorrect_guesses < max_attempts and "_" in display_word:
    print("Word: " + " ".join(display_word))
    guess = input("Enter a letter: ").lower()

    if len(guess) != 1 or not guess.isalpha():
        print("⚠️  Please enter a single alphabet letter.\n")
        continue

    if guess in guessed_letters:
        print("🔁 You already guessed that letter. Try another.\n")
        continue

    guessed_letters.append(guess)

    if guess in secret_word:
        print("✅ Correct guess!\n")
        for idx, letter in enumerate(secret_word):
            if letter == guess:
                display_word[idx] = guess
    else:
        incorrect_guesses += 1
        print(f"❌ Wrong guess! Attempts left: {max_attempts - incorrect_guesses}\n")

# End of game result
if "_" not in display_word:
    print("🎉 Congratulations! You guessed the word:", secret_word)
else:
    print("😢 You ran out of attempts. The word was:", secret_word)
