# apuntes
apuntes sobre Python, Linux y el Work de Hacking

import pygame
import random

# Inicialización de Pygame
pygame.init()

# Configuración de la pantalla
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Guitar Hero")

# Colores
white = (255, 255, 255)
black = (0, 0, 0)

# FPS
clock = pygame.time.Clock()
fps = 60

# Notas y teclas
note_width = 100
note_height = 20
note_speed = 5
notes = []

# Generar notas aleatorias
def generate_note():
    x_position = random.choice([150, 300, 450, 600])
    note = pygame.Rect(x_position, 0, note_width, note_height)
    notes.append(note)

# Main Loop
running = True
while running:
    screen.fill(black)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Generar nota cada cierto tiempo
    if random.randint(1, 100) > 98:
        generate_note()

    # Mover notas
    for note in notes:
        note.y += note_speed
        pygame.draw.rect(screen, white, note)
        if note.y > screen_height:
            notes.remove(note)

    # Actualizar la pantalla
    pygame.display.flip()
    clock.tick(fps)

pygame.quit()
