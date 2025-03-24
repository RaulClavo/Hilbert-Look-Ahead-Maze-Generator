from hilbertcurve.hilbertcurve import HilbertCurve
import math, random, pygame

pygame.init()

cells, screen_size = 16, 400  # Las celdas solo pueden ser potencias de 2.
grid_size, offset = screen_size // cells, (screen_size - (screen_size // cells) * cells) // 2
hilbert_curve = HilbertCurve(int(math.log(cells, 2)), 2)
points = hilbert_curve.points_from_distances(list(range(2 ** (2 * int(math.log(cells, 2))))))

def hilbert_to_coords(x, y):
    return x * grid_size + grid_size // 2 + offset, y * grid_size + grid_size // 2 + offset

def draw():
    screen.fill((255, 255, 255))
    connected_points = set()

    for i in range(1, len(points)):
        x, y = points[i]
        if i in connected_points or not (x in {0, cells-1} or y in {0, cells-1}): continue
        for adj in [(x-1, y), (x+1, y), (x, y-1), (x, y+1)]:
            if (adj[0] in {0, cells-1} and 0 <= adj[1] < cells) or (adj[1] in {0, cells-1} and 0 <= adj[0] < cells):
                pygame.draw.line(screen, (0, 0, 0), hilbert_to_coords(*points[i]), hilbert_to_coords(*adj), 2)
                connected_points.add(i)

    for i in range(1, len(points)):
        if i in connected_points: continue
        x, y = points[i]
        valid_adjacents = [adj for adj in [(x-1, y), (x+1, y), (x, y-1), (x, y+1)] if 0 <= adj[0] < cells and 0 <= adj[1] < cells and points.index([adj[0], adj[1]]) > i]
        if valid_adjacents:
            pygame.draw.line(screen, (0, 0, 0), hilbert_to_coords(*points[i]), hilbert_to_coords(*random.choice(valid_adjacents)), 2)
            connected_points.add(i)
    pygame.display.flip()

screen = pygame.display.set_mode((screen_size, screen_size))
pygame.display.set_caption("HLAMG")
draw()

running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT: running = False
        elif event.type == pygame.KEYDOWN and event.key == pygame.K_RETURN: draw()
    pygame.time.wait(500)
