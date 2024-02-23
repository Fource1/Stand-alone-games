# Stand-alone-games
class MazeGame:
    def __init__(self, maze):
        self.maze = maze

    def play(self):
        player_position = (0, 0)
        end_position = (len(self.maze) - 1, len(self.maze[0]) - 1)

        while player_position != end_position:
            print_maze(self.maze, player_position)
            direction = input("Enter direction (up/down/left/right): ").lower()

            new_position = self.get_new_position(player_position, direction)
            if self.is_valid_move(new_position):
                player_position = new_position
            else:
                print("Invalid move. Try again.")

        print("Congratulations! You reached the end of the maze.")

    def get_new_position(self, position, direction):
        x, y = position
        if direction == "up":
            return x - 1, y
        elif direction == "down":
            return x + 1, y
        elif direction == "left":
            return x, y - 1
        elif direction == "right":
            return x, y + 1

    def is_valid_move(self, position):
        x, y = position
        return 0 <= x < len(self.maze) and 0 <= y < len(self.maze[0]) and self.maze[x][y] == 1

def print_maze(maze, player_position):
    for i, row in enumerate(maze):
        for j, cell in enumerate(row):
            if (i, j) == player_position:
                print("P", end=" ")
            elif cell == 1:
                print(".", end=" ")
            else:
                print("#", end=" ")
        print()

# Example usage
maze = [
    [1, 0, 1, 1, 1],
    [1, 1, 1, 0, 1],
    [0, 0, 1, 1, 1],
    [1, 0, 0, 0, 1],
    [1, 1, 1, 1, 1]
]

game = MazeGame(maze)
game.play()
