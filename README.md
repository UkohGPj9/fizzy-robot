fizzy-robot
===========

import random
import sys

#sys.setrecursionlimit(2500)

#global vars
current_room = 0
item_list = ["piece of string"]
box_2_taken = 0
goop_in_room_4 = 1
robot_defeated = 0
robots_number = random.randint(1,10)
ladder_taken = 0
first_time_in_room_6 = 1
crowbar_taken = 0
crate_opened = 0
ladder_used = 0
vault_7_open = 0

def intro_description():
    print """
                
     ~~~~~~~~~~~~      ****************************      ~~~~~~~~~~~~~~~~~~~~~~
    You open your eyes and find that you are staring upwards at a hatch in the ceiling.
    As it happens, you have no recollection of how you got here, where \"here\" is, or even your name.
    Oh well. You decide to do something about this, if only because you're bored.
    """
    room_1_description()

###ROOM 1
def room_1_description():
    if ladder_used == 0:
        print """
    This is an unremarkable empty white room with four walls and a door in each. There is also a hatch
    in the ceiling.
    """
        room_1_actions()
    elif ladder_used == 1:
        print """
    This is an unremarkable empty white room with four walls and a door in each. There is also a hatch
    in the ceiling, with a ladder stationed underneath.
    """
        room_1_actions()

def room_1_actions():
    global current_room
    current_room = 1
    if ladder_used == 0:
        print """
    What do you want to do?
    1. Go north
    2. Go east
    3. Go south
    4. Go west
    5. Use an item.
    """
        action = raw_input("\n> ")
        if action == "1":
            room_6_description()
        elif action == "2":
            room_2_description()
        elif action == "3":
            room_4_description()
        elif action == "4":
            room_3_description()
        elif action =="5":
            display_inventory()
        else:
            print "Choose better. (just type a number, dummy)"
            room_1_actions()
    if ladder_used == 1:
        print """
    What do you want to do?
    1. Go north
    2. Go east
    3. Go south
    4. Go west
    5. Use an item.
    6. Climb the ladder.
    """
        action = raw_input("\n> ")
        if action == "1":
            room_6_description()
        elif action == "2":
            room_2_description()
        elif action == "3":
            room_4_description()
        elif action == "4":
            room_3_description()
        elif action =="5":
            display_inventory()
        elif action == "6":
            room_8_description()
        else:
            print "Choose better. (just type a number, dummy)"
            room_1_actions()
###ROOM 2
def room_2_description():
    print "\nAnother empty white room. This time with a box in the corner."
    room_2_actions()

def room_2_actions():
    global current_room
    current_room = 2
    print """
    What do you want to do?
    1. Go back west
    2. Open the box.
    3. Use an item.
    """
    action = raw_input("\n> ")
    if action == "1":
        room_1_description()
    elif action == "2":
        take_room2_box()
    elif action == "3":
        display_inventory()
    else:
        print "Choose better. (just type a number, dummy)"
        room_2_actions()

def take_room2_box():
    global box_2_taken
    if box_2_taken == 0:
        print "\nYou open the box and take out two pairs of odd plastic boots. One pair is green, the other is red."
        print "\n\t~Items added to inventory: green boots, red boots."
        item_list.append("green boots")
        item_list.append("red boots")
        box_2_taken = 1
        room_2_description()
    if box_2_taken == 1:
        print "\nThat box is empty. Since you already took the boots, it is going to remain empty. Move along."
        room_2_description()
        
###ROOM 3
def room_3_description():
  print "\nYou find yourself standing in the center of a room with many leather-bound books."
	print "This room smells of rich mahogany. There is one door in the east wall."
	print "On a table in the corner sits a box with a bold label that says \"Do NOT open.\" The NOT is underlined."
	room_3_actions()

def room_3_actions():
    global current_room
    current_room = 3
    print """
    What do you want to do?
    1. Go back east.
    2. Open the box. 
    3. Use an item.
    """
    action = raw_input("\n> ")
    if action == "1":
        room_1_description()
    elif action == "2":
        print "\nIgnoring the VERY CLEAR LABEL, you open the box."
        print "\nWHat are you, a complete gibbering idiot?"
        print "\nA swarm of horrible, mutated, acid-spewing space-bee-weasels pours out of the box."
        print "\nThey melt your face and you die a horrible agonizing death. Or do you...?"
        intro_description()
    elif action == "3":
        display_inventory()
    else:
		print "Choose better. (just type a number, dummy)"
		room_3_actions()
		
###ROOM 4
def room_4_description():
	if goop_in_room_4 == 1:
		print """
A dingy gray room, with doors in both the north and south walls. 
Noticeable is the pool of green funny-smelling green goop covering the floor.
Somehow you managed to accidentally jump onto the one patch of clean floor. 
If you want to use either door now, you'll definitely have to step in the goop.
"""
		room_4_actions()
	if goop_in_room_4 == 0:
		print "\nA dingy gray room with doors in both the north and south walls."
		print "Noticeable is the fact that there is no longer a foul-smelling pool of green goop covering the floor."
		room_4_actions()

def room_4_actions():
	global current_room
	current_room = 4
	print """
    What do you want to do?
	1. Go north.
	2. Go south.
	3. Use an item.
	"""
	action = raw_input("\n> ")
	if action == "1":
		if goop_in_room_4 == 1:
			print "\nYou knew you shouldn't have stepped in that goop. As soon as you touch the goop, "
			print "it seeps into your skin and melts you from the inside out."
			print "Not a pleasant way to go, and now you're dead. Or are you...?"
			intro_description()
		elif goop_in_room_4 == 0:
			print "\nIt's a good thing all that nasty goop is gone. You step across the room carefree."
			room_1_description()
	elif action == "2":
		if goop_in_room_4 == 1:
			print "\nYou knew you shouldn't have stepped in that goop. As soon as you touch the goop,"
			print "it seeps into your skin and melts you from the inside out."
			print "Not a pleasant way to go, and now you're dead. Or are you...?"
			intro_description()
		elif goop_in_room_4 == 0:
			print "\nIt's a good thing al that nasty goop is gone. You step across the room carefree."
			room_5_description()
	elif action == "3":
		display_inventory()
	else:
		print "Choose better. (just type a number, dummy)"
		room_4_actions()
		
###ROOM 5
def room_5_description():
	global current_room 
	current_room = 5
	if robot_defeated == 0:
		robot_room()
	elif robot_defeated == 1:
		print "\nThis is the room where you defeated NumberTron5000. It's a pretty boring-looking room now."
		if ladder_taken == 0:
			print "With the once mighty robot out of the way, you notice a folded stepladder in the corner."
			room_5_actions()
		if ladder_taken == 1:
			room_5_actions()
			
def room_5_actions():
	global ladder_taken
	if ladder_taken == 0:
		print """
	What do you want to do?
	1. Take the ladder.
	2. Go back north.
	3. Use an item.
	"""
		action = raw_input("\n> ")
		if action == "1":
			print "You take the ladder."
			print "\n\t~Item added to inventory: ladder."
			item_list.append("ladder")
			ladder_taken = 1
		elif action == "2":
			room_4_description()
		elif action == "3":
			display_inventory()
        else:
			print "Choose better. (just type a number, dummy)"
			room_5_actions()
	if ladder_taken == 1:
		print """
	What do you want to do?
	1. Go back north.
	2. Use an item.
    """
		action = raw_input("\n> ")
		if action == "1":
			room_4_description()
		elif action == "2":
			display_inventory()
        else:
			print "Choose better. (just type a number, dummy)"
			room_5_actions()

def robot_room():
	print "Obstructing your view further into this room is a blocky metallic structure."
	print "At first distracted by the marvelously sharp implements protruding from the device,"
	print "you do not realize that this is in fact a robot until it addresses you:"
	print "\n\"Greetings fleshbag. You stand before NumberTron5000, the most powerful generator of random numbers"
	print "this universe has ever known. Once I generate a number, it will be so powerfully random"
	print "that you could never guess it. Ever. What integer between 1 and 10 (inclusive) am I thinking of?"
	print "You had better use numeral integers to answer. Other inputs make me angry.\""
	robot_room_actions()
	
def robot_room_actions():
	print """
	What do you do?
	1. Guess a number
	2. Use an item
	"""
	action = raw_input("\n> ")
	if action == "1":
		guessing_game_input()
	elif action == "2":
		display_inventory()
	else:
		print "Choose better. (just type a number, dummy)"
		robot_room_actions()
	
def guessing_game_input():
		raw_guess = raw_input("What is your guess?\n> ")
		guessing_game_result(raw_guess)

def guessing_game_result(raw_guess):
	global robot_defeated
	try:
		your_guess = int(raw_guess)
		if your_guess == robots_number:
			print """
NumberTron5000: "Bleep! Bloop! A fleshbag has successfully guessed NumberTron5000's number! 
That is illogical. Self destructing in 3...2...1..." The robot begins to vibrate and shake. 
A buzzing sound emanates and grows in volume until with a bang and a shower of sparks it falls to the ground in parts.
		"""
			robot_defeated = 1
			room_5_description()
		elif your_guess > 10 or your_guess < 1:
			print """
		NumberTron5000: "Do you now know how to count from 1 to 10? Foolish fleshbag.
		Numbertron5000 is THIS CLOSE to terminating you. You do NOT want a description of how.
		"""
			robot_room_actions()
		else:
			print """
		NumberTron5000: "That is not my random number. Your foolish efforts amuse me. Guess again fleshbag."
		"""
			robot_room_actions()
	except ValueError:
		print """
		NumberTron5000: "Do you not know what NUMERALS and INTEGERS are? Foolish fleshbag."
		NumberTron5000 is THIS CLOSE to terminating you. You do NOT want a description of how.
		"""
		robot_room_actions()

###ROOM	6
def room_6_description():
	global current_room
	global first_time_in_room_6
	current_room = 6
	if first_time_in_room_6 == 1:
		print "\nYou notice with some pleasure that the walls in this room are a stunning beige color."
		print "You briefly pause to wonder why you find the color beige so attractive. Finding no answer, you move on mentally."
		print "\nThere are doors set in the north and south walls."
		first_time_in_room_6 = 0
		room_6_actions()
	elif first_time_in_room_6 == 0:
		print "\nThere are doors set in the north and south walls of this room. Lovely beige color, those walls."
		room_6_actions()
		
def room_6_actions():
	global crowbar_taken
	if crowbar_taken == 0:
		print "You also notice that there's a sturdy-looking crowbar leaning in one corner."
		print """
		What do you want to do?
		1. Take the crowbar. 
		2. Go north.
		3. Go south.
		4. Use an item.
		"""
		action = raw_input("\n>")
		if action == "1":
			print "You take the crowbar."
			print "\n\t~Item added to inventory: crowbar/"
			item_list.append("crowbar")
			crowbar_taken = 1
			room_6_description()
		elif action == "2":
			room_7_description()
		elif action == "3":
			room_1_description()
		elif action == "4":
			display_inventory()
		else:
			print "Choose better. (just type a number, dummy)"
			room_5_actions()
	elif crowbar_taken == 1:
		print """
		What do you want to do?
		1. Go north.
		2. Go south.
		3. Use an item.
		"""
		action = raw_input("\n>")
		if action == "1":
			room_7_description()
		elif action == "2":
			room_1_description()
		elif action == "3":
			display_inventory()
		else:
			print "Choose better. (just type a number, dummy)"
			room_5_actions()
				
###ROOM7
def room_7_description():
	global current_room
	current_room = 7
	if vault_7_open == 0:
		print "\nThat door opened into a small antechamber, where you face a steel vault door."
		print "A doormat in front of the door reads:"
		print "\t<>Portal Room. Authorized Access Only.<>"
		print "Set into the face of the door is a button labelled ACCESS and a magnetic swipe."
		room_7_actions()
	elif vault_7_open == 1:
		print "\nYou pass through the antechamber into the room beyond."
		print "\nThe walls, floor, and ceiling of this room pulse to a slow beat, turning from"
		print "bright white through pink to red and back again."
		print "The room is empty, save for a perfectly circular mesh inlay in the center of the room."
		room_7_actions()
		
def room_7_actions():
	if vault_7_open == 0:
		print """
	What do you want to do?
	1. Press the button.
	2. Step back into the beige room.
	3. Use an item.
	"""
		action = raw_input("\n>")
		if action == "1":
			print "\nFor the brief moment that your finger touches the button, your body begins to tingle."
			print "Almost instantaneously after that you hear the sound of a static discharge, and..."
			room_3_description()
		elif action == "2":
			room_6_description()
		elif action == "3":
			display_inventory()
		else:
			print "Chhose better. (just type a number, dummy)"
			room_7_actions()
	elif vault_7_open == 1:
		print """
	What do you want to do?
	1. Step into the circle.
	2. Go back to the beige room.
	3. Use an item.
		"""
		action = raw_input("\n>")
		if action == "1":
			print "As you step into the circle, your feet begin to tingle."
			print "A klaxon blares, and a recorded voice bellows \"IMPROPER FOOTWEAR DETECTED. BEGINNING DISASSEMBLY.\""
			print "An agonizing pain takes over where the tingling left off, and you fel as though every"
			print "particle of your being is being set on fire."
			print "And now you're dead. Or are you...?"
			room_1_description()
		elif action == "2":
			room_6_description()
		elif action == "3":
			display_inventory()

			
###ROOM 8
def room_8_description():
	global current_room
	current_room = 8
	print "\nAfter climbing up the ladder and through the hatch, you find yourself in a small compartment above the white room below."
	print "The only thing in the compartment is a small crate."
	room_8_actions()

def room_8_actions():
	print """
	What do you want to do?
	1. Go down the ladder.
	2. Open the crate.
	3. Use an item.
	"""
	action = raw_input("\n>")
	if action == "1":
		room_1_description()
	elif action == "2":
		if crate_opened == 0:
			print "\nThe top of the crate is fastened shut firmly. You consider prying it open with your fingers,"
			print "but that will almost certainly lead to you breaking a nail, and you decide there must be a better way."
			room_8_actions()
		elif crate_opened == 1:
			print "\nYou already used the crowbar to open the crate and get the lot. Ain't nothin' there now, move along."
			room_8_actions()
	elif action == "3":
		display_inventory()
	else:
		print "Choose better. (just type a number, dummy)"
        room_8_actions()

###inventory & utility functions

def display_inventory():
	print "What item do you want to use? You have:"
	print item_list
	x = raw_input("\n>")
	item_use_check(x)
	
def item_use_check(x):
	print "\n\tYou chose to use %s." % x
	if x not in item_list:
		print "\n\tThat's not an item you have. Moron.\n"
		display_inventory()
	else:
		use_item(x)

def use_item(x):
	global ladder_used
	global robot_defeated
	global crate_opened
	global vault_7_open
	global goop_in_room_4
	if x == "piece of string":
		print "\n\tYou play with the string. I guess that was fun?"
		room_redirector(current_room)
	elif x == "green boots":
		if current_room == 4:
			print "\nYou put on the green boots and step gingerly into the green goop."
			print "\nAs you shuffle forward, the boots absorb the goop and simultaneously rot away into nothingness."
			goop_in_room_4 = 0
			print "\n\t~Item removed from inventory: green boots."
			item_list.remove("green boots")
			print "\nUnder the goop was a small plastic button which you pick up."
			print "\nIt says 'Universal Robot Hacking Device.' Sounds convenient."
			print "\n\t~Item added to inventory: robo-clicker-thingy."
			item_list.append("robo-clicker-thingy")
			room_4_description()
		elif current_room != 4:
			print "\n\tThose don't do anything here."
			room_redirector(current_room)
	elif x == "red boots":
		if current_room == 7:
			print "\nYou put on the red boots and step onto the teleport pad."
			print "\nWhoosh! ZIP! Biff! Off onto your next adventure."
			print "\Also, you think that piece of string is gone now."
			print "\n\n\t\t***VICTORY***"
			print "Game exiting now."
			exit(0)
		elif current_room != 7:
			print "\n\tThose don't do anythng here."
			room_redirector(current_room)
	elif x == "robo-clicker-thingy":
		if current_room !=5:
			print "\n\tThat doesn't do anythng here."
			room_redirector(current_room)
		elif current_room == 5:
			print "\nNumberTron5000 emits an undignified and extremely unrobotlike squawk and disappears with a POP."
			robot_defeated = 1
			room_5_description()
	elif x == "ladder":
		if current_room != 1:
			print "\n\tThat doesn't do anythng here."
			room_redirector(current_room)
		elif current_room == 1:
			print "\nYou use the ladder to climb through the hatch into the room above."
			print "\n\t~Item removed from inventory: ladder."
			item_list.remove("ladder")
			ladder_used = 1
			room_8_description()
	elif x == "crowbar":
		if current_room != 8:
			print "\n\tThat doesn't do anythng here."
			room_redirector(current_room)
		elif current_room == 8:
			if crate_opened == 0:
				print "\n\tYou use the crowbar to pry off the crate's lid, revealing a padded interior."
				print "\tWhile making a surreptitious fist-pump, you pull out a plastic dongle,"
				print "\tintriguingly labelled: \"Teleport Room KeyCard //single use// --Authorized Personnel Only--\""
				print "\n\t~Item added to inventory: keycard."
				item_list.append("keycard")
				crate_opened = 1
				room_8_actions()
			elif crate_opened == 1:
				print "\nWhat do you want to do, smash the crate? Cause you can't. Move along."
				room_8_actions()
	elif x == "keycard":
		if current_room != 7:
			print "\n\tThose don't do anythng here."
			room_redirector(current_room)
		elif current_room == 7:
			print "\n\tYou swipe the keycard and press the button."
			print "\tThe door abruptly vanishes, as does the keycard out of your hand."
			print "\n\t~Item removed from inventory: keycard."
			item_list.remove("keycard")
			vault_7_open = 1
			room_7_description()
			
def room_redirector(x):
	if x == 1:
		room_1_description()
	if x == 2:
		room_2_description()
	if x == 3:
		room_3_description()
	if x == 4:
		room_4_description()
	if x == 5:
		room_5_description()
	if x == 6:
		room_6_description()
	if x == 7:
		room_7_description()
	if x == 8:
		room_8_actions()
	
	
print "\n\t\t***NOTE: To exit this game at any time, use CTRL+C. Your progress will not be saved."	
	
intro_description()

