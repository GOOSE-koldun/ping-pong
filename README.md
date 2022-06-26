# ping-pong
это проект сделанный на языке програмирования python. проект представляет из себя программу для игры двух человек в игру пин-понг, где левой ракеткой управляет первый игрок с помощью клавиш "w" и "s", и правой второй игрок на клавиши "up" и "down".
import pygame
import sys

pygame.init()

BLACK = (0, 0, 0)
WHITE = (225, 225, 225)
 
posY_block1 = 150
posY_block2 = 150
posX_circle = 80
posY_circle = 150

circle_right = True
circle_top = True

speed = 5
screenWidth = 800
screenHeight = 400
 
screen = pygame.display.set_mode((screenWidth, screenHeight))
clock = pygame.time.Clock()

while True:
    clock.tick(60)
    screen.fill(BLACK)
 
    pressed_keys = pygame.key.get_pressed()
    if pressed_keys[pygame.K_UP]:
        if posY_block1 > 0:
            posY_block1 -= speed
    if pressed_keys[pygame.K_DOWN]:
        if posY_block1 + 100 < screenHeight:
            posY_block1 += speed
    if pressed_keys[pygame.K_w]:
        if posY_block2 > 0:
            posY_block2 -= speed
    if pressed_keys[pygame.K_s]:
        if posY_block2 + 100 < screenHeight:
            posY_block2 += speed
    if posX_circle - 50 <= 0:
        circle_right = True
    if posY_circle - 50 <= 0:
        circle_top = False
    elif posY_circle + 50 >= screenHeight:
        circle_top = True
    if circle_right:
        posX_circle += speed
    else:
        posX_circle -= speed
    if circle_top:
        posY_circle -= speed
    else:
        posY_circle += speed
    if posY_block1 <= posY_circle <= posY_block1 + 100 and screenWidth - 20 <= posX_circle + 50 <= screenWidth:
        circle_right = False
    if posY_block2 >= posY_circle >= posY_block2 + 100 and screenWidth - 20 >= posX_circle + 50 >= screenWidth:
        circle_left = False
    elif posX_circle + 50 > screenWidth:
        pygame.quit()
        sys.exit()

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    pygame.draw.rect(screen, WHITE, (0, posY_block2, 20, 100))
    pygame.draw.rect(screen, WHITE, (780, posY_block1, 20, 100))
    pygame.draw.circle(screen, WHITE, (posX_circle, posY_circle), 50)
    pygame.display.update()
