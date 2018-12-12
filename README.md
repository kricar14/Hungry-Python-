# Hungry-Python-

"""To start the game---> click Kernel ---> restart & run all.
Within this game a moving snake will appear that can be controlled using the arrow buttons (up, down, left, right) on your keyboard.You can quit the Game anytime by pressing 'q' on the keyborad. Food icons will appear one at a time, in order to eat them run over them with the snake. Each piece of food that is collected results in the snake's body increasing length. The game is over when the snake runs into itself. One feature that is different from the original snake game is that the snake is able to run off the screen and teleport to the opposite side, back into view."""

import turtle

import random

import os

from time import sleep


class Food():
    
    def __init__ (self, food_character, terminal): 
        
        self.food_character = food_character
        
        self.terminal = terminal
        
        
    def FoodShape(self):
        
        """Creates the shapes of the food. 
    
        Parameters
        ----------
        shapes : string
            various shapes (images) available through turtle module. 
        food : function
            using random method selects food shape from shapes.
    
        Returns
        -------
        food : string with associated image 
            The result of food function.
        """  
        
        shapes = ["arrow", "turtle", "circle", "triangle", "classic"]
        
        food = random.choice(shapes)
        
        return food
    
    
    def FoodColor(self): 
        
        """Sets color of food. 
    
        Parameters
        ----------
        colors : string
            various colors available through turtle module. 
        food : function
            using random method selects food color from colors.
    
        Returns
        -------
        food : string with associated color
            The result of food function. 
        """ 
        
        colors = ["red", "blue", "green", "yellow", "orange", "purple","violet", "pink"]
        
        food = random.choice(colors)
        
        return food
    
    
    def FoodStamp(self, food_character): 
        
        """Places the food on the screen. 
    
        Parameters
        ----------
        stamp : function
            using turtle method makes image of food_character. 
    
        Returns
        -------
        stamp : image
            The result of shapes combined with colors. 
        """ 
        
        stamp = self.food_character.stamp
        
        stamp
        
        
class Snake(Food):  
    
    def __init__ (self, food_character, character, terminal):
        
        super().__init__(food_character, terminal) 
        
        self.food_character = food_character
        
        self.character = character
        
        self.terminal = terminal
        
        
    def SpawnSnake(self, character, terminal): 
        
        """Spawns the snake onto the game screen (terminal)."""
        
        self.character.penup()
        
        self.character.shape("square")
        
        
class Controls(Snake):
    
    """Sets up directions the snake can move on the screen. 
    
    Parameters
    ----------
    collision_count : int or float
        Input to length_step and speed_step, used to grow and speed up snake 
        in response to collisions with food
             
    length_step : int or float
        Input to the LengthStepper, sets the initial length of the snake & increases 
        in response to CollosionCount to grow the snake.
            
    speed_step : int or float
        Input to the SpeedStepper, sets the initial speed of the snake to a high speed.
        
    speed_brake : int or float
        Delays snake's movement, is reduced in response to CollosionCount to speed 
            up the snake, is used because it allows finer speed control than speed_step. 
    """
    
    collision_count = 0
    
    length_step = 3
    
    speed_step = 2
    
    speed_brake = 32
    
     
    def __init__ (self, food_character, character, terminal):
        
        super().__init__(food_character, character, terminal) 
        
        self.food_character = food_character
        
        self.character = character
        
        self.terminal = terminal
        
        
    def Left(self):
        
        """Turns Snake to face the left side of the window. 
    
        Parameters
        ----------
        if self.character.heading()!=0: : int
            Checks if snake is not on reverse heading, restricts 
            snake from turning back on its own track. 
            
        self.character.speed(0) : function
            Turtle function, sets snake to max speed.
            
        self.character.setheading(180) : function
            Turtle function, sets snake to max speed.
            
        self.character.speed(self.speed_step) : function 
            Turtle function, returns snake to play speed as defined by speed_step function.
         
        """  
        
        if self.character.heading()!=0:
            
            self.character.speed(0)
            
            self.character.setheading(180)
            
            self.character.speed(self.speed_step)
            
            
    def Right(self):
        
        """Turns Snake to face the right side of the window. 
    
        Parameters
        ----------
        if self.character.heading()!=0: : int
            Checks if snake is not on reverse heading, restricts 
            snake from turning back on its own track. 
            
        self.character.speed(0) : function
            Turtle function, sets snake to max speed.
            
        self.character.setheading(180) : function
            Turtle function, sets snake to max speed.
            
        self.character.speed(self.speed_step) : function 
            Turtle function, returns snake to play speed as defined by speed_step function.
         
        """   
        if self.character.heading()!=180:
            
            self.character.speed(0)
            
            self.character.setheading(0)
            
            self.character.speed(self.speed_step) 
            
            
    def Up(self):
        
        """Turns Snake to face the top of the window. 
    
        Parameters
        ----------
        if self.character.heading()!=0: : int
            Checks if snake is not on reverse heading, restricts 
            snake from turning back on its own track. 
            
        self.character.speed(0) : function
            Turtle function, sets snake to max speed.
            
        self.character.setheading(180) : function
            Turtle function, sets snake to max speed.
            
        self.character.speed(self.speed_step) : function 
            Turtle function, returns snake to play speed as defined by speed_step function.
         
        """ 
        
        if self.character.heading()!=270:
            
            self.character.speed(0)
            
            self.character.setheading(90)
            
            self.character.speed(self.speed_step)  
            
            
    def Down(self):
        
        """Turns Snake to face the bottom of the window. 
    
        Parameters
        ----------
        if self.character.heading()!=0: : int
            Checks if snake is not on reverse heading, restricts 
            snake from turning back on its own track. 
            
        self.character.speed(0) : function
            Turtle function, sets snake to max speed.
            
        self.character.setheading(180) : function
            Turtle function, sets snake to max speed.
            
        self.character.speed(self.speed_step) : function 
            Turtle function, returns snake to play speed as defined by speed_step function.
         
        """ 
        
        if self.character.heading()!=90:
            
            self.character.speed(0)
            
            self.character.setheading(270)
            
            self.character.speed(self.speed_step)
            
            
    def Reset(self):
        
        """Returns Snake to center of the window if it gets lost off screen. 
    
        Parameters
        ----------
    
        self.character.speed(0) : function
            Turtle function, sets snake to max speed.
            
        self.character.goto(0,0) : function
            Turtle function, places head of snake to (0,0) on same heading & speed.
            
        self.character.speed(self.speed_step) : function 
            Turtle function, returns snake to play speed as defined by speed_step function.
         
        """ 
        
        self.character.speed(0)
        
        self.character.goto(0,0)
        
        self.character.speed(self.speed_step)
        
        
    def Quit(self):
        
        """Quits game. 
    
        Parameters
        ----------
    
        self.terminal.bye() : function
            Turtle function, terminates window.
        
        """
        
        self.terminal.bye()

        
class PlayGame(Controls): 
    
    sList = []
    
    def __init__ (self, food_character, character, terminal):
        
        super().__init__(food_character, character, terminal) 
        
        self.food_character = food_character
        
        self.character = character
        
        self.terminal = terminal
        
        
    def InsertFood(self, food_character):
        
        """Inserts a single piece of randomly generated food at a random point in the window. 
    
        Parameters
        ----------
    
        X : function
            Selects a random point between the left and right side of the screen 
            at 20 pixel intervals.  Does not select within 60 pixels of the edge 
            to prevent food being generated off screen
            
        Y : function
            Selects a random point between the top and bottom side of the screen 
            at 20 pixel intervals.  Does not select within 60 pixels of the edge 
            to prevent food being generated off screen
            
        foodPos : list
            Puts X & Y into a coordinate list for placing the food.
            
        self.food_character.speed(0) : function
            Turtle function, sets food to max speed.
            
        self.food_character.penup() : function
            Turtle function, prevents turtle from drawing a line on the way to the 
            food's location.
           
        self.food_character.setpos(foodPos) : function 
            Turtle function, moves cursor to coordinates called in foodPos.
            
        self.food_character.shape(self.FoodShape()) : function 
            Turtle function, sets shape of cursor to the shape randomly selected by FoodShape() function.
        
        self.food_character.color(self.FoodColor()) : function 
            Turtle function, sets color of cursor to the shape randomly selected by FoodColor() function.
        
        self.FoodStamp(self.food_character) : function 
            Turtle function, stamps the food_character cursor on the window.
        """ 
        
        X = random.randrange(-self.terminal.screensize()[0]+60, self.terminal.screensize()[0]-60, 20) 
        
        Y = random.randrange(-self.terminal.screensize()[1]+60, self.terminal.screensize()[1]-60, 20)
        
        foodPos = [X,Y]
        
        self.food_character.speed(0)
        
        self.food_character.penup()
        
        self.food_character.setpos(foodPos)
        
        self.food_character.shape(self.FoodShape())
        
        self.food_character.color(self.FoodColor())
        
        self.FoodStamp(self.food_character)
        
    #inspired from check_bounds from A4 but has been altered   
    def CheckBounds(self):
        
        """Checks if the snake has run off the screen and repositions it to the opposite 
        side if it has, the function is repeated to check if the snake has run off the 
        sides of the screen or if the snake has run off the top/bottom of the screen. 
    
        Parameters
        ----------
    
        if abs(self.character.position()[0]) >= abs(self.terminal.screensize()[0]-50) : function
            Checks if the X value of the snake is larger than the X value of the edge of the window. 
            
        self.food_character.speed(0) : function
            Turtle function, sets food to max speed.
            
        self.character.hideturtle() : function
            Turtle function, hides the snakes head for transport across the window.
            
        self.character.speed(0) : function
            Turtle function, sets food to max speed.
           
        self.character.goto((self.character.position()[0]*-1),self.character.position()[1]) : function 
            Turtle function, moves cursor to the inverse X coordinate and the same Ycoordinate.
            
        self.character.showturtle() : function 
            Turtle function, sets the cursor to visible to resume gameplay.
        
        self.character.speed(self.speed_step) : function 
            Turtle function, returns snake to play speed as defined by speed_step function.

        """ 
        
        if abs(self.character.position()[0]) >= abs(self.terminal.screensize()[0]-50):
            
            self.character.speed(0)
            
            self.character.hideturtle()
            
            self.character.goto((self.character.position()[0]*-1),self.character.position()[1])
            
            self.character.showturtle()
            
            self.character.speed(self.speed_step)  
            
        if abs(self.character.position()[1]) >= abs(self.terminal.screensize()[1]-50):
            
            self.character.speed(0)
            
            self.character.hideturtle()
            
            self.character.goto((self.character.position()[0]),self.character.position()[1]*-1)
            
            self.character.showturtle()
            
            self.character.speed(self.speed_step) 
            
            
    def SnakePos(self, character):
        
        """Creates inital orientation of snake. 
    
        Parameters
        ----------
        self.character.position() : function
            uses method in turtle to initialize orientation of snake's inital movement
            
        Returns
        -------
        self.character.position() : List
            coordinates of the snake.
        """
        
        return self.character.position()
    
    
    def foodPos(self, food_character):
           
        """Sets point on screen where food is positioned. 
    
        Parameters
        ----------
        self.food_character.position() : function
            uses method in turtle to initalize spot on screen for food
             
        Returns
        -------
        self.food_character.position() : List
            coordinates of the food. 
        """
        
        return self.food_character.position()
    
    
    def CollisionDetect(self, food_character, character):
        
        """Creates collision detection for snake running into food
        and snake running into itself. 
    
        Parameters
        ----------
        food : function
            runs self.food_character
        snake :function
             
        Returns
        -------
        self.food_character.position() : List
            Returns the X, Y coordinates of the food. 
        """
        
        food = self.foodPos(self.food_character)
        
        snake = self.SnakePos(self.character)

        
        if round((food[0]),0) == round((snake[0]),0) and round((food[1]),0) == round((snake[1]),0):
            
            self.terminal.delay(0)
            
            self.character.speed(0)
            
            self.food_character.clearstamp(self.InsertFood(food_character))
            
            self.CollisionCounter()
            
            self.LengthStepper()
            
            self.SpeedStepper()
            
            self.terminal.delay(self.speed_brake)
            
            self.character.speed(self.speed_step)
            
            
    def CollisionCounter(self):
        
        self.collision_count += 1
        
        return self.collision_count
    
    
    def LengthStepper(self):   
        
        if (self.collision_count%2) == 0:
            
            self.length_step += 3
            
            
    def SpeedStepper(self):  
        
        if (self.collision_count%10) == 0:
            
            self.speed_brake -= 2
            
            
    def GameOver (self):
        """ Ends the game if the snake runs into itself, creates game over screen
            and then exists out of game screen. 
    
        Parameters
        ----------
        sPosX : function
            gets and rounds the snake head's x coordinates to a whole number
            
        sPosY :function
            gets and rounds the snake head's y coordinates to a whole number
            
        sPos : list
            makes the X,Y list
            
        self.character.write() : function
            uses list to make text
            
        self.terminal.bye() : function
            method to exit screen
             
        Returns
        -------
        sPos : List
            makes rounded X, Y list. 
            
        self.character.write() :
            creates game over screen
            
        self.terminal.bye():
            exits game screen
        """
        
        sPosX = round((self.character.xcor()),0)
        
        sPosY = round((self.character.ycor()),0)
        
        sPos = (sPosX, sPosY)
        
        #This loop ends the game if the snake runs into itself
        if len(self.sList)>= self.length_step and sPos in self.sList: 
            
            self.character.speed(0)
            
            self.character.hideturtle()
            
            self.character.goto(0,0)
            
            for stamp in self.sList:
                
                self.character.clearstamps(1) 
                   
            self.character.write('Game Over', move=True, align="center", font=("Impact", 70, "bold"))
            
            sleep(2)
            
            self.terminal.bye()  
            
            
    def MoveSnake(self, character, terminal): 
        
        """Uses classes Up, Down, Right, Left, Reset, and Quit as parameter for the 
        .onkey ,method from turtle, to associate arrows, q, and spacebar with commands. 
    
        Parameters
        ----------
        sPosX : function
            gets and rounds the snake head's x coordinates to a whole number
            
        sPosY :function
            gets and rounds the snake head's y coordinates to a whole number
            
        sPos : list
            makes the X,Y list
             
        Returns
        -------
        sPos : List
            makes rounded X, Y list. 
        """
           
        self.SpawnSnake(self.character, self.terminal)
        
        while True: 
            
            try:
                
                sPosX = round((self.character.xcor()),0)
                
                sPosY = round((self.character.ycor()),0) 
                
                sPos = (sPosX, sPosY) 
                
                self.GameOver()
                
                #add the snake head position to the body
                self.sList.append(sPos) 
                
                #clear and add new food when snake eats
                self.CollisionDetect(self.food_character, self.character) 
                
                #sets base speed of snake
                self.character.speed(self.speed_step)
                
                #set brake on speed of snake - used to increase speed
                self.terminal.delay(self.speed_brake) 
                
                # moves the snakes head forward 20 px
                self.character.forward(20)
                
                #stamps the snake's head onto the window
                self.character.stamp() 
                
                #controls the length of the snake
                if len(self.sList)>self.length_step:  
                    
                    self.character.clearstamps(1)
                    
                    del(self.sList[0])
                    
                self.CheckBounds()
                
                self.terminal.onkey(Controls(self.food_character, self.character, self.terminal).Left, "Left")
                
                self.terminal.onkey(Controls(self.food_character, self.character, self.terminal).Right, "Right")
                
                self.terminal.onkey(Controls(self.food_character, self.character, self.terminal).Up, "Up")
                
                self.terminal.onkey(Controls(self.food_character, self.character, self.terminal).Down, "Down")
                
                self.terminal.onkey(Controls(self.food_character, self.character, self.terminal).Reset, "space")
                
                self.terminal.onkey(Controls(self.food_character, self.character, self.terminal).Quit, "q")
                
                self.terminal.listen() 
                
            except:
                
                os._exit(0)
                

random.seed()

#parameters of screen
turtle.setup(width=700, height=500, startx=0, starty=0)

window = turtle.Screen()

#prints title of game
window.title("Hungry Python!")

#sets game screen background
window.bgcolor("lightgreen")

tess = turtle.Turtle()

snack = turtle.Turtle()

ssssnack = PlayGame(snack, tess, window)

ssssnack.InsertFood(snack)

ssss = PlayGame(snack, tess, window)

ssss.MoveSnake(tess, window)

window.mainloop()
