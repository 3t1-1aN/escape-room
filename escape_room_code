#Room Class:
#Represents each room in the game.
#Stores the room's name, description, and exits.
#Provides methods to get exits and display room information.

class Room:
    def __init__(self, name, description, exits, items=None, key=None):
        self.name = name
        self.description = description
        self.exits = exits
        self.items = items if items else []
        self.key = key
        
    def get_exits(self, direction):
        return self.exits.get(direction)
    
    def display(self):
        #displays the name, description, and exits
        print(f'[Current location: {self.name}]\n')
        print(self.description)
        if self.name != 'porch':
            print("Exits:", ", ".join(self.exits))
        else:
            print('')
        if self.items:
            print("Items in the room:")
            for item in self.items:
                print(f"- {item.name}")
         
#Player Class:
#Keeps track of the user's current room.
#Handles movement between rooms and displays the room's details.

class Player:
#    initialize player's location:
    def __init__(self, starting_room):
#        set the self.current_room to the starting room
        self.current_room = starting_room
        self.inventory = []  # list to store player's inventory items
        
    def look_around(self):
        if self.current_room.name == 'Porch':
            print("\nCongratulations, you escaped!")
            exit()
        self.current_room.display()
        
#    function move(keeps track of players movement):
    def move(self, direction):
#        set a next room variable to get the direction the user wants to go and
#        update the current location to that room.
        next_room = self.current_room.get_exits(direction)
#        run an if else check to see the direction in the next_room varable is 
#        valid.

        try:
            if next_room.key == None or (next_room.key is None or next_room.key in self.inventory):
                self.current_room = next_room
                print(f"you move in direction {direction}")
            elif next_room.key != None and next_room.key.name == 'pant' and next_room.key.name not in self.inventory:
                print("\nThe door is locked!")
            elif next_room.key != None and next_room.key.name == 'flashlight' and next_room.key.name not in self.inventory:
                print("\nThere is no power in this room. You can't see anything")
                
        except:
                print("You can't go that way\n")
                
    def take_item(self, item_name, can_take=False):
#        Picks up an item from the room.
        for item in self.current_room.items:
            if item.name == item_name:
                if item.can_take == True:
                    self.inventory.append(item)
                    self.current_room.items.remove(item)
                    print(f"\nYou picked up the {item_name}.")
                    print(f'{item.description}')
                else:
                    print(f'You can\'t take item {item_name}')
                    return
        print(f"\nThere is no {item_name} here.")

    def use_item(self, item_name):
#       Uses an item from the inventory.
        for item in self.current_room.items:
            if item.name == item_name:
                if item.interact():
                    self.inventory.append(item)
                    self.current_room.items.remove(item)
                    if item.name == 'flashlight':
                        print(f"\nYou picked up the flashlight.")
                    elif item.name == 'pant':
                        print('you picked up a key')
                return
        print(f'Don\'t know what {item_name} is.')
        
class Item:
#   A class to represent an item in the game.
    def __init__(self, name, interact_message=None, can_take=False):
        self.name = name
        self.interact_message = interact_message  # Message when the item is interacted with
        self.can_take = can_take

    def interact(self):
#       Perform an interaction with the item.
        if self.interact_message:
            print(self.interact_message)
        #else:
        #    print(f"You can't do anything special with the {self.name}.")
        if self.name == 'gasoline':
            print('You died')
            exit()
        return self.can_take

'''Game Class:
Manages the game setup, including room creation and linking.
Controls the game loop (where the user interacts with the game).

    initialize the room and player(making self.player = Player(starting_room=living_room):
    
    function setup():
        make the different rooms as dictionaries with its name, description, 
        and exits
        
    function play():
        displays game name
        displays backstory
        displays the room the user starts in
        a while loop that asks the user for where they want to go:
            an if check for 'quit':
                display end quote
            an elif check for directions:
                call self.player and pass in direction they want to go'''
                
class Game:
    def __init__(self):
        self.rooms = {}
        self.player = None
    
    def setup(self):
        note = Item("note","The note reads: It is there within the bookshelf")
        flashlight = Item('flashlight', 'You can now check out the gameroom', can_take=True)
        gasoline = Item('gasoline', 'You breathed in the toxic fumes.')
        lamp = Item('lamp', 'You pull the lamp and the west-side bookshelf opens up revealing another room(enter room with \'view hidden room\')')
        washingMachine = Item('washing machine', 'A washing machine with a spinning drum and a load of laundry on top')
        pant = Item('pant','you find a key in one of the pant pockets', can_take = True)
        #escapeKey = Item(None, '&-<', can_take=True)
        couch = Item('couch', 'There is a soft and warm couch')
        coffeeTable = Item('coffee table', 'There is a coffee mug, book and plate on top of it')
        tv = Item('tv', 'The TV is turned on with a picture of a dog playing fetch')
        rug = Item('rug', 'The rug is soft and warm')
        showpieces = Item('showpieces', 'There are books, movies, and relics on the mantle')
        kitchenSink = Item('kitchen Sink')
        stove = Item('stove', 'There is a stove with a burner and a pan of oil on top')
        oven = Item('oven', 'There is an oven with an oven tray in it')
        countertop = Item('countertop', 'There is a giant countertop with a sink, stove, and oven in between')
        arcadeMachine = Item('arcade machine', 'Just a massive arcade machine')
        pinballMachine = Item('pinball Machine', 'Just a pinball machine')
        poolTable = Item('pool table', 'A pooltable set with the sticks, 8-ball and triangular formation balls')
        sink = Item('sink', 'A bathroom sink')
        bathtub = Item('bathtub', 'A bathroom bathtub with a tub faucet on the right side')
        shower = Item('shower', 'A shower with shapoo bottles and soaps')
        toilet = Item('toilet', 'A toilet with a toilet paper dispenser next to it')
        towelRack = Item('towel rack', 'a place to place dry or wet towels')
        steamer = Item('steamer', 'a place to to relax')
        walkInCloset = Item('walk-in closet', 'a large room with lots of clothes hangers and racks')
        bed = Item('bed', 'Resting place')
        fountain = Item('fountain', 'a big bubbly water fountain')



        option1 = Room(name = "West-side Livingroom",
                    description = '',
                    exits = {})
        
        option2 =Room(name = "East-side Livingroom", 
                    description = '', 
                    exits = {})
        
        livingroom = Room(name = "Livingroom",
                    description = "You are in a giant dimly lit room with a several couches, coffee tables, a giant TV, and exotic rugs and counter tops with various showpieces on top",
                    exits = {},
                    items = [couch, coffeeTable, tv, rug, showpieces])
        
        kitchen = Room(name = "Kitchen", 
                    description = "You are in a marble kitchen with wooden cabnets and a giant polished granite island in the middlewith high chairs around it. There is a massive counter top with a sink, stove, and oven in between. Finally in the south end, there is a giant glass window looking out back", 
                    exits = {},
                    items = [kitchenSink, stove, oven, countertop])
        
        gameroom = Room(name = "Gameroom", 
                    description = "See lots of old arcade type games, pinball machines, a tv, and pool table with a note attached to it",
                    exits = {},
                    items = [arcadeMachine, pinballMachine, tv, poolTable, note],
                    key = flashlight)
        
        laundry = Room(name = "Laundry", 
                    description = "This is a smaller room with a washer, a dryer, some clothe baskets, and some racks on the wall with the detergents and stuff",
                    exits = {},
                    items = [washingMachine, pant])
        
        library = Room(name = "Library", 
                    description = "A room filled with books. A peculiar wall lamp on the east-side wall catches your eye",
                    exits = {},
                    items = [lamp])
        
        garage = Room(name = "Garage", 
                    description = "This room has a pungant gasoline smell to it. It has racks lining the walls with all sorts of vehicle parts and tools and all sorts of liquid bottles. The left wall has a giant switch board", 
                    exits = {},
                    items = [gasoline, flashlight])
        
        bathroom = Room(name = "Bathroom", 
                    description = "A big white washroom with a sink, tub, shower, toilet, towel racks, and a steamer", 
                    exits = {},
                    items = [sink, bathtub, shower, toilet, towelRack, steamer])
        
        bedroom = Room(name = "Bedroom", 
                    description = "a big room with exotic rug on the ground, a large walk-in closet on the east-side wall, windows, and a king size bed", 
                    exits = {},
                    items = [rug, walkInCloset, bed])
        
        porch = Room(name = "Porch", 
                    description = "the deck attached to the outside world surrounded by a forest of trees.",
                    exits = {},
                    key = pant)
        
        backyard = Room(name = "Backyard", 
                    description = "Leads to a giant backyard with lots of skillfully sculpted bushes and a big fountain in the center. It is surrounded by big palm trees and thick foliage fencing it.", 
                    exits = {},
                    items = [fountain])
        
        
        option1.exits = {"north":gameroom,"west":laundry,"south":library, "east":livingroom}
        option2.exits = {"south":kitchen,"east":bathroom, "west":livingroom}
        livingroom.exits = {"north":porch,"south":backyard,"east":option2,"west":option1}
        kitchen.exits = {"north":option1, "south":backyard}
        gameroom.exits = {'south':option1}
        laundry.exits = {"east":option1}
        library.exits = {"north":option1}
        garage.exits = {"north":bathroom}
        bathroom.exits = {"north":bedroom,"south":garage,"west":option2}
        bedroom.exits = {"south":bathroom}
        porch.exits = {'freedom': 'freedom'}
        backyard.exits = {"north":livingroom}
        
        #store rooms in game
        self.rooms = {option1:"West-side Livingroom", option2:"East-side Livingroom", livingroom:"Livingroom", kitchen:"Kitchen", gameroom:"Gameroom", laundry:"Laundry", library:"Library", garage:"Garage", bathroom:"Bathroom", bedroom:"Bedroom", porch:"Porch", backyard:"Backyard"}
        self.player = Player(starting_room=livingroom)
        
    def play(self):
        state = False
        print("Welcome to Ravenswood escape. Your goal is to escape from the mansion that you have been locked in. to go in a direction, just input the direction name. To check out an item, input 'view' + item name. Good luck!")
        self.player.look_around()
        
        while True:
            command = input('\nWhat do you want to do? \n').strip().lower()
            parts = command.split()
            if command == "quit":
                print("\nThanks for playing!")
                break
            elif command == "view hidden room":
                print("\nYour curiosity gets the better of you and you enter a secret lab room. The radioactive elements stored there over time instantly kill you.")
                exit()
            elif command in ["north", "south", "east", "west"]:
                self.player.move(command)
                self.player.look_around()
            elif parts[0] == "view" and len(parts) > 1:
                self.player.use_item(" ".join(parts[1:]))
            else:
                print("\nInvalid command. Try 'north', 'south', 'east', 'west', or 'quit'.")
game = Game()
game.setup()
game.play()
