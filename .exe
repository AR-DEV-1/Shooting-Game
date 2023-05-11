# Import the libraries
import pygame
import random

# Initialize pygame
pygame.init()

# Create the screen
screen = pygame.display.set_mode((800, 600))

# Set the title and icon
pygame.display.set_caption("Shooting Game")
icon = pygame.image.load("icon.png")
pygame.display.set_icon(icon)

# Define the colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)

# Define the player class
class Player:

  # Initialize the player with an image, a position, and a speed
  def __init__(self, image, x, y, speed):
    self.image = pygame.image.load(image)
    self.x = x
    self.y = y
    self.speed = speed

  # Define the method to draw the player on the screen
  def draw(self):
    screen.blit(self.image, (self.x, self.y))

  # Define the method to move the player left or right
  def move(self):
    # Get the pressed keys
    keys = pygame.key.get_pressed()

    # Move left if the left arrow key is pressed and the player is not at the left edge
    if keys[pygame.K_LEFT] and self.x > 0:
      self.x -= self.speed

    # Move right if the right arrow key is pressed and the player is not at the right edge
    if keys[pygame.K_RIGHT] and self.x < 736:
      self.x += self.speed

# Define the bullet class
class Bullet:

  # Initialize the bullet with an image, a position, a speed, and a state
  def __init__(self, image, x, y, speed):
    self.image = pygame.image.load(image)
    self.x = x
    self.y = y
    self.speed = speed
    self.state = "ready" # ready means the bullet is not fired yet

  # Define the method to draw the bullet on the screen
  def draw(self):
    screen.blit(self.image, (self.x + 16, self.y + 10))

  # Define the method to fire the bullet from the player's position
  def fire(self):
    # Change the state to fired
    self.state = "fired"

    # Set the bullet's position to the player's position
    self.x = player.x
    self.y = player.y

  # Define the method to move the bullet up
  def move(self):
    # Move up if the state is fired and the bullet is not at the top edge
    if self.state == "fired" and self.y > 0:
      self.y -= self.speed

    # Reset the state to ready if the bullet is at the top edge
    elif self.y <= 0:
      self.state = "ready"

# Define the enemy class
class Enemy:

  # Initialize the enemy with an image, a position, a speed, and a direction
  def __init__(self, image, x, y, speed):
    self.image = pygame.image.load(image)
    self.x = x
    self.y = y
    self.speed = speed
    self.direction = "right" # right means moving right

  # Define the method to draw the enemy on the screen
  def draw(self):
    screen.blit(self.image, (self.x, self.y))

  # Define the method to move the enemy left or right and down
  def move(self):
    # Move right if the direction is right and the enemy is not at the right edge
    if self.direction == "right" and self.x < 736:
      self.x += self.speed

      # Change the direction to left if the enemy is at the right edge and move down by 40 pixels
      if self.x >= 736:
        self.direction = "left"
        self.y += 40

    # Move left if the direction is left and the enemy is not at the left edge  
    elif self.direction == "left" and self.x > 0:
      self.x -= self.speed

      # Change the direction to right if the enemy is at the left edge and move down by 40 pixels 
      if self.x <= 0:
        self.direction = "right"
        self.y += 40

# Define a function to check collision between two objects using their positions and sizes 
def is
# Define a function to check collision between two objects using their positions and sizes
def is_collision(x1, y1, x2, y2, size):
  # Calculate the distance between the centers of the objects
  distance = ((x1 - x2) ** 2 + (y1 - y2) ** 2) ** 0.5

  # Return True if the distance is less than or equal to the size, False otherwise
  return distance <= size

# Define a function to show the score on the screen
def show_score():
  # Create a font object
  font = pygame.font.SysFont("Arial", 32)

  # Render the score text
  score_text = font.render(f"Score: {score}", True, WHITE)

  # Draw the score text on the screen at the top left corner
  screen.blit(score_text, (10, 10))

# Define a function to show the game over message on the screen
def show_game_over():
  # Create a font object
  font = pygame.font.SysFont("Arial", 64)

  # Render the game over text
  game_over_text = font.render("GAME OVER", True, RED)

  # Draw the game over text on the screen at the center
  screen.blit(game_over_text, (200, 250))

# Create an instance of the player with an image, a position, and a speed
player = Player("player.png", 370, 480, 5)

# Create an instance of the bullet with an image, a position, a speed, and a state
bullet = Bullet("bullet.png", player.x, player.y, 10)

# Create a list of enemies with random images, positions, and speeds
enemies = []
for i in range(6):
  enemy_image = random.choice(["enemy1.png", "enemy2.png", "enemy3.png"])
  enemy_x = random.randint(0, 736)
  enemy_y = random.randint(50, 150)
  enemy_speed = random.randint(1, 4)
  enemy = Enemy(enemy_image, enemy_x, enemy_y, enemy_speed)
  enemies.append(enemy)

# Initialize the score to zero
score = 0

# Create a clock object to control the frame rate
clock = pygame.time.Clock()

# Start the game loop
running = True
while running:

  # Fill the screen with black color
  screen.fill(BLACK)

  # Handle the events
  for event in pygame.event.get():

    # Quit the game if the user clicks the close button
    if event.type == pygame.QUIT:
      running = False

    # Fire the bullet if the user presses the space key and the bullet is ready
    elif event.type == pygame.KEYDOWN:
      if event.key == pygame.K_SPACE and bullet.state == "ready":
        bullet.fire()

  # Move the player
  player.move()

  # Move the bullet
  bullet.move()

  # Move the enemies
  for enemy in enemies:
    enemy.move()

    # Check if the enemy has reached the bottom edge
    if enemy.y >= 440:

      # Show the game over message and end the game loop
      show_game_over()
      running = False

    # Check if there is a collision between the bullet and the enemy
    elif is_collision(bullet.x +16 , bullet.y +10 , enemy.x +32 , enemy.y +32 ,32):

      # Reset the bullet state to ready and increase the score by one
      bullet.state = "ready"
      score +=1

      # Respawn the enemy at a random position and speed 
      enemy.x = random.randint(0 ,736)
      enemy.y = random.randint(50 ,150)
      enemy.speed = random.randint(1 ,4)
