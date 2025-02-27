
import pygame
import random

# Initialize pygame
pygame.init()

# Game constants
WIDTH, HEIGHT = 800, 600
BALL_RADIUS = 15
HOOP_X, HOOP_Y = 700, 200
GRAVITY = 0.5

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
ORANGE = (255, 165, 0)

# Set up display
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Basketball Game")

# Ball properties
ball_x, ball_y = 100, HEIGHT - 100
ball_dx, ball_dy = 0, 0
shooting = False

# Game loop
running = True
while running:
    screen.fill(WHITE)
    
    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.MOUSEBUTTONDOWN and not shooting:
            mx, my = pygame.mouse.get_pos()
            ball_dx = (mx - ball_x) / 10  # Adjust velocity based on click
            ball_dy = (my - ball_y) / 10
            shooting = True

    # Ball physics
    if shooting:
        ball_x += ball_dx
        ball_y += ball_dy
        ball_dy += GRAVITY  # Gravity effect
        
        # Collision with ground
        if ball_y + BALL_RADIUS >= HEIGHT:
            shooting = False
            ball_x, ball_y = 100, HEIGHT - 100
            ball_dx, ball_dy = 0, 0
    
    # Draw ball
    pygame.draw.circle(screen, ORANGE, (int(ball_x), int(ball_y)), BALL_RADIUS)
    
    # Draw hoop
    pygame.draw.rect(screen, BLACK, (HOOP_X, HOOP_Y, 10, 50))
    
    # Update display
    pygame.display.flip()
    
    # Frame rate
    pygame.time.delay(30)

pygame.quit()
