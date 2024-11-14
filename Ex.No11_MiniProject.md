# Ex.No: 11  Mini Project 
### DATE:                                                                            
### REGISTER NUMBER : 212221240014
### AIM: To implement the Pong game in Python using the turtle

### Algorithm:
~~~
1. Initialize game window, paddles, ball, and score display.
2. Define flag-based movement functions for paddles:
    - On key press, set movement flag to True.
    - On key release, set movement flag to False.
3. Define `move_paddles()` to check movement flags periodically, updating paddle positions if needed.
4. Main game loop:
    a. Update ball position.
    b. Check for top/bottom boundary collisions and reverse vertical direction if necessary.
    c. Check for left/right boundary collisions:
        - Reset ball to center, reverse direction, update score.
        - Display updated score.
    d. Check for paddle collisions:
        - If ball is within paddle range, reverse horizontal direction.
5. Repeat loop continuously for game dynamics.

~~~
### Program:
~~~
import turtle as t
import os

# Player scores
playerAscore = 0
playerBscore = 0

# Paddle movement flags
left_paddle_up = False
left_paddle_down = False
right_paddle_up = False
right_paddle_down = False

# Create a window
window = t.Screen()
window.title("The Pong Game")
window.bgcolor("black")  # Background color changed to black
window.setup(width=800, height=600)
window.tracer(0)

# Left paddle
leftpaddle = t.Turtle()
leftpaddle.speed(0)
leftpaddle.shape("square")
leftpaddle.color("white")
leftpaddle.shapesize(stretch_wid=5, stretch_len=1)
leftpaddle.penup()
leftpaddle.goto(-350, 0)

# Right paddle
rightpaddle = t.Turtle()
rightpaddle.speed(0)
rightpaddle.shape("square")
rightpaddle.color("white")
rightpaddle.shapesize(stretch_wid=5, stretch_len=1)
rightpaddle.penup()
rightpaddle.goto(350, 0)

# Ball
ball = t.Turtle()
ball.speed(1)
ball.shape("circle")
ball.color("red")
ball.penup()
ball.goto(5, 5)
ballxdirection = 0.2
ballydirection = 0.2

# Pen for scorecard update
pen = t.Turtle()
pen.speed(0)
pen.color("blue")
pen.penup()
pen.hideturtle()
pen.goto(0, 260)
pen.write("Player A: 0   Player B: 0", align="center", font=('Arial', 24, 'normal'))

# Paddle movement functions
def move_paddles():
    if left_paddle_up:
        leftpaddle.sety(leftpaddle.ycor() + 20)
    if left_paddle_down:
        leftpaddle.sety(leftpaddle.ycor() - 20)
    if right_paddle_up:
        rightpaddle.sety(rightpaddle.ycor() + 20)
    if right_paddle_down:
        rightpaddle.sety(rightpaddle.ycor() - 20)

    # Schedule the next paddle move check
    window.ontimer(move_paddles, 20)

# Key press handlers
def leftpaddleup_press():
    global left_paddle_up
    left_paddle_up = True

def leftpaddleup_release():
    global left_paddle_up
    left_paddle_up = False

def leftpaddledown_press():
    global left_paddle_down
    left_paddle_down = True

def leftpaddledown_release():
    global left_paddle_down
    left_paddle_down = False

def rightpaddleup_press():
    global right_paddle_up
    right_paddle_up = True

def rightpaddleup_release():
    global right_paddle_up
    right_paddle_up = False

def rightpaddledown_press():
    global right_paddle_down
    right_paddle_down = True

def rightpaddledown_release():
    global right_paddle_down
    right_paddle_down = False

# Assign keys to control paddles with press and release events
window.listen()
window.onkeypress(leftpaddleup_press, 'w')
window.onkeyrelease(leftpaddleup_release, 'w')
window.onkeypress(leftpaddledown_press, 's')
window.onkeyrelease(leftpaddledown_release, 's')
window.onkeypress(rightpaddleup_press, 'Up')
window.onkeyrelease(rightpaddleup_release, 'Up')
window.onkeypress(rightpaddledown_press, 'Down')
window.onkeyrelease(rightpaddledown_release, 'Down')

# Start continuous paddle movement
move_paddles()

# Game loop
while True:
    window.update()

    # Moving the ball
    ball.setx(ball.xcor() + ballxdirection)
    ball.sety(ball.ycor() + ballydirection)

    # Border collision
    if ball.ycor() > 290:
        ball.sety(290)
        ballydirection *= -1
    if ball.ycor() < -290:
        ball.sety(-290)
        ballydirection *= -1

    # Right wall collision
    if ball.xcor() > 390:
        ball.goto(0, 0)
        ballxdirection *= -1
        playerAscore += 1
        pen.clear()
        pen.write("Player A: {}   Player B: {}".format(playerAscore, playerBscore), align="center", font=('Arial', 24, 'normal'))
        os.system("afplay wallhit.wav&")

    # Left wall collision
    if ball.xcor() < -390:
        ball.goto(0, 0)
        ballxdirection *= -1
        playerBscore += 1
        pen.clear()
        pen.write("Player A: {}   Player B: {}".format(playerAscore, playerBscore), align="center", font=('Arial', 24, 'normal'))
        os.system("afplay wallhit.wav&")

    # Paddle collision
    if (340 < ball.xcor() < 350) and (rightpaddle.ycor() - 40 < ball.ycor() < rightpaddle.ycor() + 40):
        ball.setx(340)
        ballxdirection *= -1
        os.system("afplay paddle.wav&")

    if (-350 < ball.xcor() < -340) and (leftpaddle.ycor() - 40 < ball.ycor() < leftpaddle.ycor() + 40):
        ball.setx(-340)
        ballxdirection *= -1
        os.system("afplay paddle.wav&")



~~~







### Output:

![pong game ](https://github.com/user-attachments/assets/6c7b88c8-b9ac-463d-a972-bf80086931c8)


### Result:
Thus the simple game was implemented 
