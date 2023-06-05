```python
import pygame
import random

pygame.init()

# Set up the game window
window_width, window_height = 400, 600
window = pygame.display.set_mode((window_width, window_height))
pygame.display.set_caption("Bouncy Sphere")

# Colors
black = (0, 0, 0)
white = (255, 255, 255)

# Bird properties
bird_radius = 20
bird_x = 100
bird_y = int(window_height / 2)
bird_velocity = 0
gravity = 0.6

# Pipe properties
pipe_width = 70
pipe_gap = 200
pipe_x = window_width
pipe_height = random.randint(100, 400)
pipe_speed = 3

score = 0
clock = pygame.time.Clock()

game_active = True

def display_score(score):
    font = pygame.font.Font(None, 36)
    text = font.render("Score: " + str(score), True, white)
    window.blit(text, (10, 10))

def draw_bird(x, y):
    pygame.draw.circle(window, white, (x, y), bird_radius)

def draw_pipes(x, height):
    pygame.draw.rect(window, white, (x, 0, pipe_width, height))
    pygame.draw.rect(window, white, (x, height + pipe_gap, pipe_width, window_height))

def check_collision(x, y, height):
    if x >= pipe_x and x <= pipe_x + pipe_width:
        if y <= height or y >= height + pipe_gap:
            return True
    return False

running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE:
                    bird_velocity = -10
        if event.type == pygame.MOUSEBUTTONDOWN:
            if not game_active:
                game_active = True
                bird_y = int(window_height / 2)
                bird_velocity = 0
                pipe_x = window_width
                score = 0
    
    if game_active:
        bird_y += bird_velocity
        bird_velocity += gravity
    
        window.fill(black)
        draw_bird(bird_x, bird_y)
        draw_pipes(pipe_x, pipe_height)
        display_score(score)
    
        pipe_x -= pipe_speed
    
        if check_collision(bird_x, bird_y, pipe_height):
            game_active = False
    
        if pipe_x < -pipe_width:
            pipe_x = window_width
            pipe_height = random.randint(100, 400)
            score += 1
    
        pygame.display.update()
        clock.tick(60)

pygame.quit()

```

    pygame 2.3.0 (SDL 2.24.2, Python 3.9.13)
    Hello from the pygame community. https://www.pygame.org/contribute.html



```python

```
