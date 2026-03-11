# Hello
import pygame
import sys

# Initialize Pygame
pygame.init()

# Screen dimensions and setup
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Kill Block Example")
clock = pygame.time.Clock()

# Colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)
BLUE = (0, 0, 255)

# Player setup
player_size = 40
player_pos = [WIDTH // 2, HEIGHT - player_size]
player_rect = pygame.Rect(*player_pos, player_size, player_size)
player_speed = 5

# Kill block setup
kill_block_size = 60
kill_block_pos = [WIDTH // 4, HEIGHT // 2]
kill_block_rect = pygame.Rect(*kill_block_pos, kill_block_size, kill_block_size)

# Game over flag
game_running = True


while game_running:
    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Control player movement
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player_rect.x -= player_speed
    if keys[pygame.K_RIGHT]:
        player_rect.x += player_speed
    if keys[pygame.K_UP]:
        player_rect.y -= player_speed
    if keys[pygame.K_DOWN]:
        player_rect.y += player_speed

    # Collision detection
    if player_rect.colliderect(kill_block_rect):
        print("Game Over: Player hit the kill block!")
        game_running = False

    # Drawing
    screen.fill(WHITE)
    pygame.draw.rect(screen, RED, kill_block_rect)  # Draw kill block
    pygame.draw.rect(screen, BLUE, player_rect)    # Draw player

    pygame.display.flip()
    clock.tick(60)

pygame.quit()
