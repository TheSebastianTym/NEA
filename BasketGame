from tkinter import *
import pygame
import sys
import random
import math

wind = Tk()
wind.title("Login Signup System")
wind.geometry("700x600")
wind.config(bg="#d9d9d9")
name_list=[]
password_list=[]


try:
    with open("accounts.txt", "r") as file:
        for line in file:
            name, password, Health, Speed, Jump_Strength, Throw_Vel = line.strip().split(",")
            name_list.append(name)
            password_list.append(password)
except FileNotFoundError:
    pass  # If the file doesn't exist yet, skip loading


def signup_frame():
    global signup_btn
    global login_btn
    signup_bg = Frame(height=425, width=450, bg="white")
    signup_bg.place(x=125, y=125)
    signup_btn.config(bg="white")
    login_btn.config(bg="#d9d9d9")
    def create_account():
        name=username_entry.get()
        password=password_entry.get()
        copassword=confpass_entry.get()
        #Base Stats
        Health=1000
        Speed=10.0
        Jump_Strength=10.0
        Throw_Vel=18.0
       
        #Robustness
        if name == "" and password == "":
            message_lbl=Label(signup_bg, height=2, width=25, fg="#ff5d47", text="Enter Name and Password!",
                              font=("helvectica", 13), bg="white")
            message_lbl.place(x=115, y=350)
            wind.after(2000, message_lbl.destroy)
        elif name == "":
            message_lbl=Label(signup_bg, height=2, width=25, fg="#ff5d47", text="Enter Name!",
                              font=("helvectica", 13), bg="white")
            message_lbl.place(x=115, y=350)
        elif password == "":
            message_lbl=Label(signup_bg, height=2, width=25, fg="#ff5d47", text="Enter Password!",
                              font=("helvectica", 13), bg="white")
            message_lbl.place(x=115, y=350)
        elif password!=copassword:
            message_lbl=Label(signup_bg, height=2, width=25, fg="#ff5d47", text="Passwords do not match!",
                              font=("helvectica", 13), bg="white")
            message_lbl.place(x=115, y=350)
        elif name in name_list:
            message_lbl=Label(signup_bg, height=2, width=25, fg="#ff5d47", text="Account already exists!",
                              font=("helvectica", 13), bg="white")
            message_lbl.place(x=115, y=350)
        
        #If Everything's Good
        else:
            name_list.append(name)
            password_list.append(password)
            with open("accounts.txt", "a") as file:
                file.write(f"{name},{password},{Health},{Speed},{Jump_Strength},{Throw_Vel}\n") #save as "username, password"
            message_lbl=Label(signup_bg, height=2, width=25, fg="Green", text="Account Created Successfully!",
                              font=("helvectica", 13), bg="white")
            message_lbl.place(x=115, y=350)
            print(name_list, "\n", password_list)
    #-----------------------------------------------------------
    
    #All Buttons and text
    username_text = Label(signup_bg, height=1, width=15, bg="white", fg="black", text="Username:",
                          font=("helvectica", 16), anchor="w")
    username_text.place(x=38, y=54)
    username_entry = Entry(signup_bg, width=25, bg="#b9b9b9", font=("helvectica", 20), relief=FLAT)
    username_entry.place(x=40, y=80)

    password_text = Label(signup_bg, height=1, width=15, bg="white", fg="black", text="Password:",
                          font=("helvectica", 16), anchor="w")
    password_text.place(x=38, y=134)
    password_entry = Entry(signup_bg, width=25, bg="#b9b9b9", font=("helvectica", 20), relief=FLAT)
    password_entry.place(x=40, y=160)

    confpass_text = Label(signup_bg, height=1, width=15, bg="white", fg="black", text="Confirm Password:",
                          font=("helvectica", 16), anchor="w")
    confpass_text.place(x=38, y=214)
    confpass_entry = Entry(signup_bg, width=25, bg="#b9b9b9", font=("helvectica", 20), relief=FLAT)
    confpass_entry.place(x=40, y=240)

    create_account_button=Button(signup_bg, height=1, width=11, bg="#0044ff", font=("Impact", 15),
                                 relief=FLAT, border=0, activeforeground="white", fg="white",
                                 activebackground="#0044ff", text="Create", command=create_account)
    create_account_button.place(x=285, y=305)

    haveac_btn=Button(signup_bg, height=1, width=25, bg="white", font=("helvectica", 11),
                                 relief=FLAT, border=0, activeforeground="#3396ff", fg="#3396ff",
                                 activebackground="white", text="I have an account, Go Login", command=login_frame)
    haveac_btn.place(x=20, y=285)

def login_frame():
    global signup_btn
    global login_btn
    login_bg = Frame(height=425, width=450, bg="white")
    login_bg.place(x=125, y=125)
    signup_btn.config(bg="#d9d9d9")
    login_btn.config(bg="white")
    def login_account():
        global Health1, Speed1, Jump_Strength1, Throw_Vel1
        global Health2, Speed2, Jump_Strength2, Throw_Vel2
        global name1
        name1=username1_entry.get()
        password1=password1_entry.get()
        name2 = username2_entry.get()
        password2 = password2_entry.get()
        # Load all user data from the file
        user_data = {}  # A dictionary to store user details
        try:
            with open("accounts.txt", "r") as file:
                for line in file:
                    user, passw, health, speed, jump_strength, throw_vel = line.strip().split(",")
                    user_data[user] = {
                        "password": passw,
                        "health": health,
                        "speed": speed,
                        "jump_strength": jump_strength,
                        "throw_vel": throw_vel,
                    }
        except FileNotFoundError:
            pass
        # Robustness Testing
        if not name1 or not password1 or not name2 or not password2:
            message_lbl = Label(login_bg, height=2, width=25, fg="#ff5d47", text="All fields are required!",
                                font=("helvetica", 13), bg="white")
            message_lbl.place(x=115, y=350)
            wind.after(2000, message_lbl.destroy)
            return
        # Verify both users' credentials
        if name1 in user_data and user_data[name1]["password"] == password1:
            if name2 in user_data and user_data[name2]["password"] == password2:
                # Both users are successfully logged in
                successfully_frame = Frame(height=700, width=700, bg="cyan")
                successfully_frame.place(x=0, y=0)
                success_msg = Label(successfully_frame, text="Login Successful!", font=("helvetica", 20), bg="cyan", fg="green")
                success_msg.pack(pady=20)
                print(f"User 1: {name1} Stats - {user_data[name1]}")
                Health1=user_data[name1]["health"]
                Speed1=user_data[name1]["speed"]
                Jump_Strength1=user_data[name1]["jump_strength"]
                Throw_Vel1=user_data[name1]["throw_vel"]
                print(Health1, Speed1, Jump_Strength1, Throw_Vel1)
                print(f"User 2: {name2} Stats - {user_data[name2]}")
                Health2=user_data[name2]["health"]
                Speed2=user_data[name2]["speed"]
                Jump_Strength2=user_data[name2]["jump_strength"]
                Throw_Vel2=user_data[name2]["throw_vel"]
                print(Health2, Speed2, Jump_Strength2, Throw_Vel2)
                wind.destroy()
            else:
                # Second user's credentials are invalid
                message_lbl = Label(login_bg, height=2, width=25, fg="#ff5d47", text="User 2 credentials invalid!",
                                    font=("helvetica", 13), bg="white")
                message_lbl.place(x=115, y=350)
                wind.after(2000, message_lbl.destroy)
        else:
            # First user's credentials are invalid
            message_lbl = Label(login_bg, height=2, width=25, fg="#ff5d47", text="User 1 credentials invalid!",
                                font=("helvetica", 13), bg="white")
            message_lbl.place(x=115, y=350)
            wind.after(2000, message_lbl.destroy)

    # All buttons and text
    username1_text = Label(login_bg, height=1, width=15, bg="white", fg="black", text="Username 1:",
                           font=("helvetica", 16), anchor="w")
    username1_text.place(x=38, y=54)
    username1_entry = Entry(login_bg, width=25, bg="#b9b9b9", font=("helvetica", 20), relief=FLAT)
    username1_entry.place(x=40, y=80)

    password1_text = Label(login_bg, height=1, width=15, bg="white", fg="black", text="Password 1:",
                           font=("helvetica", 16), anchor="w")
    password1_text.place(x=38, y=134)
    password1_entry = Entry(login_bg, width=25, bg="#b9b9b9", font=("helvetica", 20), relief=FLAT, show="*")
    password1_entry.place(x=40, y=160)

    username2_text = Label(login_bg, height=1, width=15, bg="white", fg="black", text="Username 2:",
                           font=("helvetica", 16), anchor="w")
    username2_text.place(x=38, y=214)
    username2_entry = Entry(login_bg, width=25, bg="#b9b9b9", font=("helvetica", 20), relief=FLAT)
    username2_entry.place(x=40, y=240)

    password2_text = Label(login_bg, height=1, width=15, bg="white", fg="black", text="Password 2:",
                           font=("helvetica", 16), anchor="w")
    password2_text.place(x=38, y=294)
    password2_entry = Entry(login_bg, width=25, bg="#b9b9b9", font=("helvetica", 20), relief=FLAT, show="*")
    password2_entry.place(x=40, y=320)

    login_account_button = Button(login_bg, height=1, width=11, bg="#0044ff", font=("Impact", 15),
                                   relief=FLAT, border=0, activeforeground="white", fg="white",
                                   activebackground="#0044ff", text="Login", command=login_account)
    login_account_button.place(x=285, y=375)

    dhaveac_btn = Button(login_bg, height=1, width=25, bg="white", font=("helvetica", 11),
                         relief=FLAT, border=0, activeforeground="#3396ff", fg="#3396ff",
                         activebackground="white", text="Create New Account", command=signup_frame)
    dhaveac_btn.place(x=30, y=375)

signup_btn=Button(height=1, width=13, bg="white", relief=FLAT, border=0, fg="black", text="Signup",
                 font=("helvectica", 20), command=signup_frame)
signup_btn.place(x=125, y=73)

login_btn=Button(height=1, width=13, bg="white", relief=FLAT, border=0, fg="black", text="Login",
                 font=("helvectica", 20), command=login_frame)
login_btn.place(x=361, y=73)

signup_frame()
wind.mainloop()




#GAME CLASSES/FUNCTIONS START HERE-------------------------------------------------




#Declaring initial variables
SCREEN_WIDTH, SCREEN_HEIGHT = 1600, 800
GROUND_LEVEL = 600
FPS=100
Health=float(Health1)
Speed1=float(Speed1)
Speed2=float(Speed2)
Jump_Strength1=float(Jump_Strength1)
Jump_Strength2=float(Jump_Strength2)
Throw_Vel1=float(Throw_Vel1)
Throw_Vel2=float(Throw_Vel2)


# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)



#Defines what a Button is
class Button():
    def __init__(self, x, y, image, scale):
        width=image.get_width()
        height=image.get_height()
        self.image=pygame.transform.scale(image, (int(width*scale), int(height*scale)))
        self.rect=self.image.get_rect()
        self.rect.topleft=(x,y)
        self.clicked=False
    def draw(self, surface):
        action=False
        
        #get mouse position
        pos=pygame.mouse.get_pos()

        #check mouseover and clicked conditions
        if self.rect.collidepoint(pos):
            if pygame.mouse.get_pressed()[0] == 1 and self.clicked==False:
                self.clicked=True
                action=True
            if pygame.mouse.get_pressed()[0] == 0:
                self.clicked=False
        
        #draw button on screen
        surface.blit(self.image,(self.rect.x,self.rect.y))

        return action




#This is how the game will run
class Game:
    def __init__(self): #Initialising Game
        pygame.init() #Initialise pygame
        self.screen=pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT)) #Generate Screen
        self.clock=pygame.time.Clock()

        self.gameStateManager=GameStateManager("mainmenu") #Starting Gamestate will be MainMenu
        

        #Declaring all types of Gamestate
        self.mainmenu=MainMenu(self.screen, self.gameStateManager)
        self.kitchen=Kitchen(self.screen, self.gameStateManager)
        self.gym_menu=Gym_Menu(self.screen, self.gameStateManager)
        self.BasketGame=BasketGame(self.screen, self.gameStateManager)
        self.Bench=Bench(self.screen, self.gameStateManager)
        self.Squat=Squat(self.screen, self.gameStateManager)
        self.Run=Run(self.screen, self.gameStateManager)

        self.states = {"mainmenu":self.mainmenu, "kitchen":self.kitchen, "bench":self.Bench, "squat":self.Squat, "run":self.Run, "gym_menu":self.gym_menu, "BasketGame":self.BasketGame}
    
    def run(self): #Running Game
        while True:
            for event in pygame.event.get(): #Checks all events
                if event.type==pygame.QUIT:
                    pygame.quit()
                    sys.exit #Closes the Game
                
                if event.type == pygame.KEYDOWN: #Checks if any keys are pressed
                    
                    if event.key == pygame.K_ESCAPE: #If Escape pressed
                        self.running = False #Exit Game
                    
                    if event.key == pygame.K_w: # If "w" pressed
                        #These players Jump
                        self.BasketGame.players[0].jump()
                        self.BasketGame.players[1].jump()
                   
                    if event.key == pygame.K_UP: # If uparrow pressed
                        #These players Jump
                        self.BasketGame.players[2].jump()
                        self.BasketGame.players[3].jump()
                    
                if event.type == pygame.KEYUP: #Checks if any keys are UNpressed
                    
                    #Checks all conditions for ball throw are correct
                    if event.key == pygame.K_w and self.BasketGame.ball.heldby is not None and self.BasketGame.ball.heldby.flip==False and self.BasketGame.ball.caught==True:
                        self.BasketGame.ball.caught=False
                        self.BasketGame.ball.shoot(self.BasketGame.right_hoop) #Throws ball at right hoop
                   
                    #Checks all conditions for ball throw are correct
                    if event.key == pygame.K_UP and self.BasketGame.ball.heldby is not None and self.BasketGame.ball.heldby.flip and self.BasketGame.ball.caught==True:
                        self.BasketGame.ball.caught=False
                        self.BasketGame.ball.shoot(self.BasketGame.left_hoop) #Throws ball at left hoop

            self.states[self.gameStateManager.get_state()].run() #Run Game state that is active

            pygame.display.update() #Update display
            self.clock.tick(FPS) #Sets Frames per second





class MainMenu:
    def __init__(self, display, gameStateManager): #Initialises MainMenu
        self.display = display
        self.gameStateManager = gameStateManager
        original_image = pygame.image.load("Green Player.png").convert_alpha()  # Load Player Image
        self.image=pygame.transform.scale(original_image, size=(200,600)) # Set dimensions
        self.image=pygame.transform.flip(self.image, True, False) #Flip Image

    def update_user_stats(self, username, new_health, new_speed, new_jump_strength, new_throw_vel):
        try:
            # Step 1: Read the content of the file
            with open("accounts.txt", "r") as file:
                lines = file.readlines()

            # Step 2: Modify the specific user's stats
            updated_lines = []
            for line in lines:
                name, password, health, speed, jump_strength, throw_vel = line.strip().split(",")
                if name == username:
                    # Update only if new values are provided, otherwise keep the old value
                    health = str(new_health) if new_health is not None else health
                    speed = str(new_speed) if new_speed is not None else speed
                    jump_strength = str(new_jump_strength) if new_jump_strength is not None else jump_strength
                    throw_vel = str(new_throw_vel) if new_throw_vel is not None else throw_vel
                # Reconstruct the line and add it to the updated list
                updated_lines.append(f"{name},{password},{health},{speed},{jump_strength},{throw_vel}\n")

            # Step 3: Write the updated content back to the file
            with open("accounts.txt", "w") as file:
                file.writelines(updated_lines)

            print(f"Stats updated successfully for user: {username}")

        except FileNotFoundError:
            print("File not found!")
        except Exception as e:
            print(f"An error occurred: {e}")

    def run(self):
        self.display.fill("red") #Make Background Red
        
        self.display.blit(self.image,(SCREEN_WIDTH//5*4,SCREEN_HEIGHT//9)) #Display Avatar

        #Displays Buttons
        if game_button.draw(self.display):
            print("Game")
            BasketGame.right_win=False
            BasketGame.left_win=False
            self.gameStateManager.set_state("BasketGame")

        if gym_button.draw(self.display):
            print("gym")
            self.gameStateManager.set_state("gym_menu")

        if kitchen_button.draw(self.display):
            print("kitchen")
            self.gameStateManager.set_state("kitchen")

        if close_button.draw(self.display):
            # Update all stats
            self.update_user_stats(name1, new_health=Health, new_speed=Speed1, new_jump_strength=Jump_Strength1, new_throw_vel=Throw_Vel1)

            
            pygame.quit()
            sys.exit()






class Kitchen: #This is the kitchen Gamestate
    def __init__(self, display, gameStateManager): #Initialises Gamestate
        self.display = display
        self.gameStateManager = gameStateManager
        self.last_update_time = pygame.time.get_ticks()
        self.update_interval = 700  # Randomize positions every 0.7 seconds
        self.active_button = None  # Track which button is currently displayed
        #Initialises all food variables
        self.foods_eaten=0
        self.burgers_eaten = 0
        self.carbs_eaten = 0
        self.proteins_eaten = 0
        self.veggies_eaten = 0

    def randomize_food_button(self): #Randomises which food type gets displayed
        food_type = random.randint(1, 100)
        if food_type <= 70:
            self.active_button = burger_button
        elif 70 < food_type <= 80:
            self.active_button = carb_button
        elif 80 < food_type <= 90:
            self.active_button = protein_button
        elif 90 < food_type <= 100:
            self.active_button = veg_button

        # Randomize position for the active button
        self.active_button.rect.topleft = (
            random.randint(button_width * 4, SCREEN_WIDTH - button_width * 4),
            random.randint(button_height * 4, SCREEN_HEIGHT - button_height * 4),
        )

    def run(self): #Runs Gamestate
        self.display.fill("red")

        if mainmenubutton.draw(self.display): #Displays exit button
            self.gameStateManager.set_state("mainmenu")

        #Checks if it's time to randomise positions
        current_time = pygame.time.get_ticks()
        if current_time - self.last_update_time > self.update_interval:
            self.last_update_time = current_time
            self.randomize_food_button()

        # Draw the active button if it exists
        if self.active_button and self.active_button.draw(self.display):
            self.foods_eaten+=1
            if self.active_button == burger_button:
                self.burgers_eaten += 1
                print(f"Burgers eaten: {self.burgers_eaten}")
            elif self.active_button == carb_button:
                self.carbs_eaten += 1
                print(f"Carbs eaten: {self.carbs_eaten}")
            elif self.active_button == protein_button:
                self.proteins_eaten += 1
                print(f"Proteins eaten: {self.proteins_eaten}")
            elif self.active_button == veg_button:
                self.veggies_eaten += 1
                print(f"Veggies eaten: {self.veggies_eaten}")
        
        #Displays counts on screen
        font = pygame.font.Font(None, 36)
        text = font.render(
            f"Burgers: {self.burgers_eaten} Carbs: {self.carbs_eaten} Proteins: {self.proteins_eaten} Veggies: {self.veggies_eaten}",
            True,
            (255, 255, 255),
        )
        self.display.blit(text, (10, 10))  # Displays text at the top-left

        if self.foods_eaten>=10: #If 10 foods are eaten
            
            #Change Health variable accordingly
            global Health
            Health+=(2*self.carbs_eaten+2*self.proteins_eaten+3*self.veggies_eaten-5*self.burgers_eaten)
            print(Health)
            #Reset Game Variables
            self.foods_eaten=0
            self.burgers_eaten=0
            self.carbs_eaten=0
            self.proteins_eaten=0
            self.veggies_eaten=0
            #Return to MainMenu
            self.gameStateManager.set_state("mainmenu")






class Gym_Menu: #Gym Menu Gamestate
    def __init__(self, display, gameStateManager): #Initialises Gamestate
        self.display = display
        self.gameStateManager = gameStateManager

    def run(self): # Runs Gamestate
        self.display.fill("red")

        #Displays Buttons
        if benchbutton.draw(self.display):
            print("bench")
            self.gameStateManager.set_state("bench") #
        
        if squatbutton.draw(self.display):
            print("squat")
            self.gameStateManager.set_state("squat")

        if runbutton.draw(self.display):
            print("run")
            self.gameStateManager.set_state("run")

        if mainmenubutton.draw(self.display):
            self.gameStateManager.set_state("mainmenu")







class Bench:
    def __init__(self, display, gameStateManager): #Initialises Gamestate
        self.display = display
        self.gameStateManager = gameStateManager # 
        self.keeprunning=True
        self.last_update_time = pygame.time.get_ticks()
        self.update_interval = 4000
        self.level=0
        self.keeprunning=True
        self.skip=False
        self.colour=(0,255,0) #
        self.bar_width=SCREEN_WIDTH-100
   
    def run(self): # Runs Gamestate
        
        global Health #Call Health
        self.multiplier=  1-(50/Health) #Sets multiplier
       
        self.display.fill("red") #Fill screen red
        
        #Draw Loading bar
        pygame.draw.rect(self.display, self.colour, pygame.Rect(50, 50, self.bar_width, 50))

        keys=pygame.key.get_pressed()
        if keys[pygame.K_SPACE]:
            self.keeprunning=True #Keep running if spacebar pressed
        
        current_time = pygame.time.get_ticks()

        #Change bar width depending on time
        self.bar_width=(SCREEN_WIDTH-100)*(1-(current_time-self.last_update_time)/self.update_interval)
        
        if current_time - self.last_update_time > self.update_interval:
            self.last_update_time = current_time
            self.level+=1
            if self.keeprunning==True:
                self.update_interval*=self.multiplier
                print(self.level)
                self.keeprunning=False
            else:
                print(self.level)
                print(f"Final level: {self.level}")
                print(self.multiplier)
                global Throw_Vel1
                Throw_Vel1+=(self.level/100)

                #Prepare settings for when gym reentered and Exit
                self.keeprunning=True
                self.level=0
                self.update_interval = 4000
                print(Throw_Vel1)
                self.gameStateManager.set_state("mainmenu")




class Squat:
    def __init__(self, display, gameStateManager): #Initialises Gamestate
        self.display = display
        self.gameStateManager = gameStateManager
        self.keeprunning=True
        self.last_update_time = pygame.time.get_ticks()
        self.update_interval = 4000
        self.level=0
        self.keeprunning=True
        self.skip=False
        self.colour=(0,255,0)
        self.bar_width=SCREEN_WIDTH-100
   
    def run(self): # Runs Gamestate
        
        global Health #Call Health
        self.multiplier=  1-(50/Health) #Sets multiplier
       
        self.display.fill("red") #Fill screen red
        
        #Draw Loading bar
        pygame.draw.rect(self.display, self.colour, pygame.Rect(50, 50, self.bar_width, 50))

        keys=pygame.key.get_pressed()
        if keys[pygame.K_SPACE]:
            self.keeprunning=True #Keep running if spacebar pressed
        
        current_time = pygame.time.get_ticks()

        #Change bar width depending on time
        self.bar_width=(SCREEN_WIDTH-100)*(1-(current_time-self.last_update_time)/self.update_interval)
        
        if current_time - self.last_update_time > self.update_interval:
            self.last_update_time = current_time
            self.level+=1
            if self.keeprunning==True:
                self.update_interval*=self.multiplier
                print(self.level)
                self.keeprunning=False
            else:
                print(self.level)
                print(f"Final level: {self.level}")
                print(self.multiplier)
                global Jump_Strength1
                Jump_Strength1+=(self.level/100)

                #Prepare settings for when gym reentered and Exit
                self.keeprunning=True
                self.level=0
                self.update_interval = 4000
                print(Jump_Strength1)

                self.gameStateManager.set_state("mainmenu")


class Run:
    def __init__(self, display, gameStateManager): #Initialises Gamestate
        self.display = display
        self.gameStateManager = gameStateManager
        self.keeprunning=True
        self.last_update_time = pygame.time.get_ticks()
        self.update_interval = 4000
        self.level=0
        self.keeprunning=True
        self.skip=False
        self.colour=(0,255,0)
        self.bar_width=SCREEN_WIDTH-100
   
    def run(self): # Runs Gamestate
        
        global Health #Call Health
        self.multiplier=  1-(50/Health) #Sets multiplier
       
        self.display.fill("red") #Fill screen red
        
        #Draw Loading bar
        pygame.draw.rect(self.display, self.colour, pygame.Rect(50, 50, self.bar_width, 50))

        keys=pygame.key.get_pressed()
        if keys[pygame.K_SPACE]:
            self.keeprunning=True #Keep running if spacebar pressed
        
        current_time = pygame.time.get_ticks()

        #Change bar width depending on time
        self.bar_width=(SCREEN_WIDTH-100)*(1-(current_time-self.last_update_time)/self.update_interval)
        
        if current_time - self.last_update_time > self.update_interval:
            self.last_update_time = current_time
            self.level+=1
            if self.keeprunning==True:
                self.update_interval*=self.multiplier
                print(self.level)
                self.keeprunning=False
            else:
                print(self.level)
                print(f"Final level: {self.level}")
                print(self.multiplier)
                global Speed1
                Speed1+=(self.level/100)
                #Prepare settings for when gym reentered and Exit
                self.keeprunning=True
                self.level=0
                self.update_interval = 4000
                print(Speed1)
        
                self.gameStateManager.set_state("mainmenu")







class BasketGame:
    def __init__(self, display, gameStateManager):
        self.display = display
        self.gameStateManager = gameStateManager
        self.clock = pygame.time.Clock()
        self.running = True
        self.right_win=False
        self.left_win=False

        # Players
        self.players = [
            Player(SCREEN_WIDTH//5, flip=False), #Player 1
            Player(SCREEN_WIDTH//5*2, flip=False), #Player 2
            Player(SCREEN_WIDTH//5*3, flip=True), #Player 3
            Player(SCREEN_WIDTH//5*4, flip=True) #Player 4
        ]
        
        # Ball
        self.ball = Ball()

        # Hoops
        self.left_hoop = Hoop(0)
        self.right_hoop = Hoop(SCREEN_WIDTH-80)
        
        # Arms
        self.arm1 = RotatingArm("Green Arm.png", self.players[0].rect.x, self.players[0].rect.centery, 40, 160)
        self.arm2 = RotatingArm("Green Arm.png", self.players[1].rect.x, self.players[1].rect.centery, 40, 160)
        self.arm3 = RotatingArm("Green Arm.png", self.players[2].rect.x, self.players[2].rect.centery, 40, 160, True)
        self.arm4 = RotatingArm("Green Arm.png", self.players[3].rect.x, self.players[3].rect.centery, 40, 160, True)

        # Scores
        self.left_hoop_score = 0
        self.right_hoop_score = 0

    def run(self):
        if self.running:
            self.update()
            self.draw()
            self.clock.tick(60)  # Cap the frame rate at 60 FPS
            if self.right_win:
                self.gameStateManager.set_state("mainmenu")
            if self.left_win:
                self.gameStateManager.set_state("mainmenu")

    

    def handle_player_collisions(self):
        # Check for collisions between all pairs of players
        for i in range(len(self.players)):
            for j in range(i + 1, len(self.players)):
                player1 = self.players[i]
                player2 = self.players[j]

                if player1.rect.colliderect(player2.rect):  # If players overlap
                    # Resolve collision by pushing them apart
                    if player1.rect.centerx < player2.rect.centerx:
                        # Player 1 is to the left of Player 2
                        overlap = player1.rect.right - player2.rect.left
                        player1.rect.right -= overlap // 2
                        player2.rect.left += overlap // 2
                    else:
                        # Player 1 is to the right of Player 2
                        overlap = player2.rect.right - player1.rect.left
                        player1.rect.left += overlap // 2
                        player2.rect.right -= overlap // 2

    def update(self):
        keys = pygame.key.get_pressed()  # Get all pressed keys
        self.players[0].update(pygame.K_a, pygame.K_d, keys, self.players[1:])
        self.players[1].update(pygame.K_a, pygame.K_d, keys, self.players[:1] + self.players[2:])
        self.players[2].update(pygame.K_LEFT, pygame.K_RIGHT, keys, self.players[:2] + self.players[3:])
        self.players[3].update(pygame.K_LEFT, pygame.K_RIGHT, keys, self.players[:3])
        
        # Handle collisions between players
        self.handle_player_collisions()

        self.ball.update(self.players)
        
        self.arm1.center_x=self.players[0].rect.centerx+10
        self.arm1.center_y=self.players[0].rect.centery-40
        self.arm2.center_x=self.players[1].rect.centerx+10
        self.arm2.center_y=self.players[1].rect.centery-40
        self.arm3.center_x=self.players[2].rect.centerx-10
        self.arm3.center_y=self.players[2].rect.centery-40
        self.arm4.center_x=self.players[3].rect.centerx-10
        self.arm4.center_y=self.players[3].rect.centery-40

        if keys[pygame.K_w]:
            self.arm1.update_angle(increase=True)
            self.arm2.update_angle(increase=True)
        else:
            self.arm1.update_angle(increase=False)
            self.arm2.update_angle(increase=False)
        
        if keys[pygame.K_UP]:
            self.arm3.update_angle(increase=True)
            self.arm4.update_angle(increase=True)
        else:
            self.arm3.update_angle(increase=False)
            self.arm4.update_angle(increase=False)

        self.check_scoring()
        
    def check_scoring(self):
        # Check for scoring in the left hoop
        if self.left_hoop.rect.colliderect(self.ball.rect):
            self.left_hoop_score += 1
            print(f"Left Hoop Scored! Score: {self.left_hoop_score}")
            self.reset_ball()

        # Check for scoring in the right hoop
        if self.right_hoop.rect.colliderect(self.ball.rect):
            self.right_hoop_score += 1
            print(f"Right Hoop Scored! Score: {self.right_hoop_score}")
            self.reset_ball()

        if self.left_hoop_score == 5:
            self.left_hoop_score=0
            self.right_hoop_score=0
            self.right_win=True

        if self.right_hoop_score == 5:
            self.left_hoop_score=0
            self.right_hoop_score=0
            self.left_win=True

    def reset_ball(self):
        self.ball.rect.centerx = SCREEN_WIDTH // 2
        self.ball.rect.bottom = 100
        self.ball.velocity_x = 0
        self.ball.velocity_y = 0
        self.ball.caught = False
        self.ball.heldby = None

    def draw(self):
        
        self.display.fill(RED)  # Clear the screen
        pygame.draw.rect(self.display, BLACK, (0, GROUND_LEVEL, SCREEN_WIDTH, SCREEN_HEIGHT - GROUND_LEVEL))  # Draw the ground
        
        for player in self.players:
            player.draw(self.display)  # Draw each player
        
        self.ball.draw(self.display)

        self.left_hoop.draw(self.display)
        self.right_hoop.draw(self.display)
       
        self.arm1.draw(self.display)
        self.arm2.draw(self.display)
        self.arm3.draw(self.display)
        self.arm4.draw(self.display)

        # Draw scores
        font = pygame.font.Font(None, 74)  # Default font with size 74
        left_score_text = font.render(f"{self.left_hoop_score}", True, WHITE)
        right_score_text = font.render(f"{self.right_hoop_score}", True, WHITE)

        self.display.blit(left_score_text, (50, 50))  # Display left hoop score
        self.display.blit(right_score_text, (SCREEN_WIDTH - 100, 50))  # Display right hoop score




#ALL CLASSES FOR GAME




class Player:
    def __init__(self, x, flip=False):
        
        #Load and scale the image
        original_image = pygame.image.load("Green Player.png").convert_alpha()  # Load Player Image
        self.image=pygame.transform.scale(original_image, size=(80,240)) # Set dimensions
        self.flip=flip
        if flip:
            self.image=pygame.transform.flip(self.image, True, False) # Flipped or not?
            self.speed = Speed1  # Movement speed
            self.jump_strength = Jump_Strength1  # Jump strength
        else:
            self.speed = Speed2  # Movement speed
            self.jump_strength = Jump_Strength2  # Jump strength
        self.rect = self.image.get_rect(midbottom=(x, GROUND_LEVEL)) # Create rectangle
        self.velocity_x = 0.0  # Horizontal velocity
        self.velocity_y = 0.0  # Vertical velocity
        self.on_ground = True  # Check if the player is on the ground
        

    def move(self, left_key, right_key, keys):
        # Handle horizontal movement
        if keys[left_key]:
            
            self.velocity_x = -float(self.speed) #Move Left when left arrow pressed
            
        elif keys[right_key]:
            self.velocity_x = float(self.speed) #Move Right when right arrow pressed
            
        else:
            self.velocity_x = 0.0 #Stationary when no action

        # APPLY horizontal movement
        self.rect.x += self.velocity_x

        # Prevent the player from leaving the screen
        if self.rect.left < 0:
            self.rect.left = 0
        elif self.rect.right > SCREEN_WIDTH:
            self.rect.right = SCREEN_WIDTH

    def jump(self):
        global Jump_Strength
        if self.on_ground:  # Only allow jumping if on the ground
            self.velocity_y = -float(self.jump_strength) #Jump Upwards
            self.on_ground = False
            print(self.jump_strength)

    def apply_gravity(self, other_players):
        self.velocity_y += 0.5  # Applying Gravity
        self.rect.y += self.velocity_y #Applying new velocity

        # Check collision with the ground
        if self.rect.bottom >= GROUND_LEVEL: # If on the ground
            self.rect.bottom = GROUND_LEVEL
            self.velocity_y = 0 # Stop falling
            self.on_ground = True 

        # Check if the player is standing on any other player
        for other_player in other_players:
            if self.rect.colliderect(other_player.rect) and self.velocity_y > 0:
                if self.rect.bottom > other_player.rect.top and self.rect.top < other_player.rect.top: #If player lands on player
                    self.rect.bottom = other_player.rect.top
                    self.velocity_y = 0 # Stop falling
                    self.on_ground = True 

    def update(self, left_key, right_key, keys, other_players):
        self.move(left_key, right_key, keys) 
        self.apply_gravity(other_players)

    def draw(self, surface):
        surface.blit(self.image, self.rect)




class Ball:
    def __init__(self):
        original_image = pygame.image.load("basketball.png").convert_alpha()  # Load Ball Image
        self.image=pygame.transform.scale(original_image, size=(60,60)) # Set Dimensions

        self.rect = self.image.get_rect(midbottom=(SCREEN_WIDTH//2, 100)) #Generate Ball at top middle of court
        self.velocity_x = 0  # Horizontal velocity
        self.velocity_y = -10  # Vertical velocity
        self.on_ground = True  # Check if the player is on the ground
        self.caught = False
        self.heldby = None
        global Throw_Vel1
        self.throw_vel = Throw_Vel1
        self.gravity = 0.3

    def apply_gravity(self):

        self.velocity_y += self.gravity  # Apply Gravity to Velocity
        self.rect.y += self.velocity_y # Apply new y velocity to position
        self.rect.x += self.velocity_x # Apply x velocity to position
    
        # Check collision with the ground
        if self.rect.bottom >= GROUND_LEVEL: #If ball hits ground
            self.rect.bottom = GROUND_LEVEL
            self.velocity_y *= -0.97 #Bounce off ground with damping
            self.velocity_x *= 0.98 #Friction slows ball down
            self.on_ground = True
        # Prevent ball from going off screen horizontally
        if self.rect.left <= 0 or self.rect.right >= SCREEN_WIDTH:
                if self.rect.left<self.velocity_x:
                    self.rect.centerx=SCREEN_WIDTH//2
                    self.rect.bottom=100
            
                if self.rect.right>SCREEN_WIDTH+self.velocity_x:
                    self.rect.right=SCREEN_WIDTH
                    self.rect.centerx=SCREEN_WIDTH//2
                    self.rect.bottom=100
                    
                self.velocity_x *= -1  # Reverse horizontal velocity
            

    def player_collision(self, player):
        if self.rect.colliderect(player.rect):
            self.heldby=player
            self.caught=True

    def shoot(self, hoop):
        x=hoop.rect.centerx-self.rect.centerx
        y=self.rect.centery-hoop.rect.top
        g=self.gravity
        switch=1

        if x<0:
            x*=-1
            switch=-1

        u_squared= (g*x**2)/(y-x)
        if u_squared<0:
            u_squared*=-1
            
        
        u=u_squared**0.5
        
        global Throw_Vel1
        if u>Throw_Vel1:
            u=Throw_Vel1
        
        #Adds random variability to the shot
        var=random.randint(-20,20)
        throw_ang=315 + var

        self.velocity_x = switch*u*math.cos(math.radians(throw_ang))
        self.velocity_y = u*math.sin(math.radians(throw_ang))
        print(u)


           
 

    def update(self, players):
        if self.caught:
            if self.heldby.flip:
                self.rect.centerx=self.heldby.rect.centerx-80
            else:
                self.rect.centerx=self.heldby.rect.centerx+80
            self.rect.centery=self.heldby.rect.centery-80
        else:
            self.apply_gravity()
        for player in players:
            self.player_collision(player)
        
        
        
    def draw(self, surface):
        surface.blit(self.image, self.rect)




class RotatingArm:
    def __init__(self, image_path, center_x, center_y, image_width, image_height,  flipped=False):
        self.center_x = center_x
        self.center_y = center_y
        self.flipped=flipped

        if self.flipped:
            self.angle=355
            self.min_angle = 355
            self.max_angle = 205
        else:
            self.angle = 5
            self.min_angle = 5
            self.max_angle = 155
        
        # Load and scale the image
        original_image = pygame.image.load(image_path)
        self.image = pygame.transform.scale(original_image, (image_width, image_height))
        self.image_width = image_width
        self.image_height = image_height

         # Keep track of the rotated image's rect
        self.rotated_image = None
        self.rotated_rect = None
        

    def update_angle(self, increase):
        if self.flipped:
            if increase and self.angle > self.max_angle:
                self.angle -= 5
            elif not increase and self.angle < self.min_angle:
                self.angle += 5
        else:
            if increase and self.angle < self.max_angle:
                self.angle += 5
            elif not increase and self.angle > self.min_angle:
                self.angle -= 5


    def draw(self, surface):
        
        # Rotate the image
        rotated_image = pygame.transform.rotate(self.image, self.angle)
        self.rotated_rect = rotated_image.get_rect(center=(self.center_x, self.center_y))

        # Calculate the new position
        pivot_x = self.center_x - rotated_image.get_width() / 2
        pivot_y = self.center_y - rotated_image.get_height() / 2

        offset_x = rotated_image.get_width() * math.sin(math.radians(self.angle)) / 2
        offset_y = rotated_image.get_height() * math.cos(math.radians(self.angle)) / 2

        draw_x = pivot_x + offset_x
        draw_y = pivot_y + offset_y

        # Blit the rotated image
        surface.blit(rotated_image, (draw_x, draw_y))

class Hoop:
    def __init__(self, x):
        #Load and scale the image
        original_image = pygame.image.load("Hoop.png").convert_alpha()  # Load Player Image
        self.image=pygame.transform.scale(original_image, size=(80,140)) # Set dimensions
        self.rect = self.image.get_rect(midleft=(x, 200)) # Create rectangle

    def draw(self, surface):
        surface.blit(self.image, self.rect)
        
class GameStateManager:
    def __init__(self, currentState):
        self.currentState=currentState
    def get_state(self):
        return self.currentState
    def set_state(self, state):
        self.currentState = state

button_img=pygame.image.load("rectangle-arrow-press.png")
kitchen_img=pygame.image.load("Kitchen_button.png")
gym_img=pygame.image.load("Gym_button.png")
play_img=pygame.image.load("Play_button.png")
exit_img=pygame.image.load("Exit_button.png")
burger_img=pygame.image.load("burger.png")
carb_img=pygame.image.load("rice.png")
protein_img=pygame.image.load("chicken-leg.png")
veg_img=pygame.image.load("broccoli.png")

button_width = button_img.get_width()
button_height = button_img.get_height()
play_width = play_img.get_width()
play_height = play_img.get_height()
exit_width = exit_img.get_width()
exit_height = exit_img.get_height()


game_button=Button(SCREEN_WIDTH//2-play_width,SCREEN_HEIGHT//2-play_height,play_img,2)
gym_button=Button(SCREEN_WIDTH//10-button_width,SCREEN_HEIGHT//9-button_height,gym_img,2)
kitchen_button=Button(SCREEN_WIDTH//10-button_width,SCREEN_HEIGHT//9*8-button_height,kitchen_img,2)
close_button=Button(SCREEN_WIDTH//2-exit_width,SCREEN_HEIGHT//5*4-exit_height,exit_img,2)
benchbutton=Button(SCREEN_WIDTH//4-button_width,SCREEN_HEIGHT//2-button_height,button_img,2)
squatbutton=Button(SCREEN_WIDTH//2-button_width,SCREEN_HEIGHT//2-button_height,button_img,2)
runbutton=Button(SCREEN_WIDTH//4*3-button_width,SCREEN_HEIGHT//2-button_height,button_img,2)
mainmenubutton=Button(SCREEN_WIDTH//10*9-button_width,SCREEN_HEIGHT//10-button_height,button_img,2)
burger_button=Button(random.randint(0, SCREEN_WIDTH-button_width),random.randint(0,SCREEN_HEIGHT-button_height),burger_img,2)
carb_button=Button(SCREEN_WIDTH//5*2-button_width,SCREEN_HEIGHT//2-button_height,carb_img,2)
protein_button=Button(SCREEN_WIDTH//5*3-button_width,SCREEN_HEIGHT//2-button_height,protein_img,2)
veg_button=Button(SCREEN_WIDTH//5*4-button_width,SCREEN_HEIGHT//2-button_height,veg_img,2)

if __name__=="__main__":
    basketball = Game()
    basketball.run()
