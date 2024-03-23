import pygame
import random

# Khởi tạo pygame
pygame.init()

# Thiết lập kích thước cửa sổ game
width, height = 640, 480
screen = pygame.display.set_mode((width, height))

# Màu sắc
white = (255, 255, 255)
red = (255, 0, 0)

# Vị trí và kích thước của con dừng
x, y = width/2, height/2
size = 50

# Điểm số
score = 0

# Tạo thời gian delay ban đầu
clock = pygame.time.Clock()
delay = 200

# Vòng lặp game
running = True
while running:
    # Xử lý sự kiện
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Kiểm tra phím nhấn
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        x -= size
    if keys[pygame.K_RIGHT]:
        x += size
    if keys[pygame.K_UP]:
        y -= size
    if keys[pygame.K_DOWN]:
        y += size

    # Kiểm tra xem con dừng có ra khỏi màn hình không
    if x < 0 or x >= width or y < 0 or y >= height:
        running = False

    # Kiểm tra xem con dừng có ăn được điểm không
    food_x, food_y = random.randrange(0, width, size), random.randrange(0, height, size)
    if x == food_x and y == food_y:
        score += 1
        delay -= 5

    # Vẽ màn hình game
    screen.fill(white)
    pygame.draw.rect(screen, red, (food_x, food_y, size, size))
    pygame.draw.rect(screen, white, (x, y, size, size))

    # Cập nhật màn hình game
    pygame.display.flip()

    # Đặt tốc độ game
    clock.tick(delay)

# Kết thúc pygame
pygame.quit()
