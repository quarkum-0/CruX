#HANGMAN GAME

import random
import time

#Starting the game.
print("    WELCOME TO THE HANGMAN GAME \n")
name = input("ENTER YOUR NAME: ")
name=name.upper()
print("WELCOME CHALLENGER " + name)
time.sleep(2)
print("STARTING THE CHALLENGE... \n")
time.sleep(1)
print("BEST OF LUCK... \n")
time.sleep(2)
print("YOU ARE GONNA NEED IT \n")
time.sleep(1)

#Function for defining of parameters.
def body():
   global display
   global word
   global count
   global already_guessed
   global length
   global play_game
   global original_word
   words_to_guess = '''ant baboon badger bat bear beaver camel cat clam cobra cougar coyote potter home
                       crow deer dog donkey duck eagle ferret fox frog goat goose hawk lion lizard llama
                       mole monkey moose mouse mule newt otter owl panda parrot pigeon python rabbit ram
                       rat raven rhino salmon seal shark sheep skunk sloth snake spider stork swan tiger
                       toad trout turkey turtle weasel whale wolf wombat zebra border image given lungs
                       doll famous rhyme damage women open close toward impassive forever human'''.split()
   word = random.choice(words_to_guess)
   original_word=word
   length = len(word)
   count = 0
   display = '_' * length
   already_guessed = []
   play_game = ""

#A function to play multiple rounds.
def play_loop():
    global play_game
    play_game = input("WOULD YOU DARE TO PLAY AGAIN? Y = YES, N = NO \n")
    play_game=play_game.lower()
    while play_game not in ["y","n"]:
        play_game = input("WOULD YOU DARE TO PLAY AGAIN? Y = YES, N = NO \n")
    if play_game == "y":
      body()
    elif play_game == "n":
        print("GOT SCARED?")
        exit()

#A function required to check if the input given are correct.
def hangman():
    global display
    global word
    global count
    limit=7
    global already_guessed
    global play_game
    global original_word
    guess = input("THIS IS THE WORD OF " + str(length) + " LETTERS: " + display + "\nENTER YOUR LETTER: ")
    guess = guess.strip()
    guess=guess.lower()
    if len(guess.strip()) == 0 or len(guess.strip()) >= 2 or guess <="9":
      print("INVALID, ONLY LETTERS ALLOWED \n")
      hangman()


    elif guess in word:
        already_guessed.extend([guess])
        index = word.find(guess)
        word = word[:index] + "_" + word[index + 1:]
        display = display[:index] + guess + display[index + 1:]
        print(display + "\n")
        
    elif guess in already_guessed:
        print("Try another letter.\n")

    else:
        count += 1

        if count == 1:
            time.sleep(1)
            print("           +-----+         \n"
                  "           |               \n"
                  "           |               \n"
                  "           |               \n"
                  "           |               \n"
                  "           |               \n"
                  "           |               \n"
                  "          =======          \n")
            print("WRONG GUESS. " + str(limit - count) + " GUESSES REMAINING\n")

        elif count == 2:
            time.sleep(1)
            print("           +-----+         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |               \n"
                  "           |               \n"
                  "           |               \n"
                  "           |               \n"
                  "          =======          \n")
            print("WRONG GUESS. " + str(limit - count) + " GUESSES REMAINING\n")

        elif count == 3:
           time.sleep(1)
           print ("           +-----+         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |               \n"
                  "           |               \n"
                  "           |               \n"
                  "          =======          \n")
           print("WRONG GUESS. " + str(limit - count) + " GUESSES REMAINING\n")

        elif count == 4:
           time.sleep(1)
           print ("           +-----+         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     O         \n"
                  "           |               \n"
                  "           |               \n"
                  "          =======          \n")
           print("WRONG GUESS. " + str(limit - count) + " GUESSES REMAINING\n")
   
        elif count == 5:
            time.sleep(1)
            print("           +-----+         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     O         \n"
                  "           |     |         \n"
                  "           |               \n"
                  "          =======          \n")
            print("WRONG GUESS. " + str(limit - count) + " GUESSES REMAINING\n")

        elif count == 6:
           time.sleep(1)
           print ("           +-----+         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     O         \n"
                  "           |    /|\        \n"
                  "           |               \n"
                  "          =======          \n")
           print("WRONG GUESS. LAST GUESS BEFORE DEATH\n")
    
        elif count == 7:
            time.sleep(1)
            print("           +-----+         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     |         \n"
                  "           |     O         \n"
                  "           |    /|\        \n"
                  "           |    / \        \n"
                  "          =======          \n")
            print("WRONG GUESS. YOU HAVE BEEN HANGED!!!\n")
            print("THE WORD WAS:",original_word,"\nLETTERS GUESSED: ",already_guessed)
            play_loop()

    if word == '_' * length:
        print("YOU JUST GOT LUCKY")
        play_loop()

    elif count != limit:
        hangman()

body()

hangman()
