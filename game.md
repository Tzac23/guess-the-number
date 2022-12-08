# "Guess the number" mini-project
# input will come from buttons and an input field
# all output for the game will be printed in the console

import simplegui
import random
import math

low = 0
high = 100

# helper function to start and restart the game
def new_game():
    # initialize global variables used in your code here
    global secret_number, count
    secret_number = random.randrange(low, high)
    print "New game. Range is from", low, "to", high
    count = int(math.ceil(math.log(high + 1, 2)))
    print "Number of remaining guesses is", count


# define event handlers for control panel
def range100():
    # button that changes the range to [0,100) and starts a new game 
    global low, high
    low = 0
    high = 100
    new_game()

def range1000():
    # button that changes the range to [0,1000) and starts a new game     
    global low, high
    low = 0
    high = 1000
    new_game()
    
def input_guess(guess):
    global count
    guess = int(guess)
    print "Guess was", guess
    count -= 1
    if count > 0:
        print "Number of remaining guesses is", count
        if guess == secret_number:
            print "Correct!"
            new_game()
        elif guess < secret_number:
            print "Higher!"
        else:
            print "Lower!"
    elif count == 0 and guess == secret_number:
        print "Correct!"
        new_game()
    else:
        print "You ran out of guesses. Number was", secret_number
        new_game()
    
# create frame
frame = simplegui.create_frame('Guess the Number', 100, 200)

# register event handlers for control elements and start frame
button100 = frame.add_button("Range is [0, 100)", range100, 200)
button1000 = frame.add_button("Range is [0, 1000)", range1000, 200)
inp = frame.add_input('Your Guess:', input_guess, 50)

frame.start()

# call new_game 
new_game()


