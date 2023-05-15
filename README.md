# Step 1: Set up the Board
board = [[' ', ' ', ' '],
         [' ', ' ', ' '],
         [' ', ' ', ' ']]


# Step 2: Print the Board
def print_board():
    for row in board:
        print(' | '.join(row))
        print('-----------')


# Step 3: Accept Player Input
def get_move(player):
    row = int(input("Enter the row (0-2): "))
    col = int(input("Enter the column (0-2): "))

    # Validate the input
    if row < 0 or row > 2 or col < 0 or col > 2:
        print("Invalid move. Please enter values between 0 and 2.")
        return get_move(player)

    if board[row][col] != ' ':
        print("That position is already occupied. Please choose an empty position.")
        return get_move(player)

    return row, col


# Step 4: Update the Board
def make_move(player, row, col):
    board[row][col] = player


# Step 5: Check for a Winner
def check_winner():
    # Check rows
    for row in board:
        if row.count(row[0]) == len(row) and row[0] != ' ':
            return row[0]

    # Check columns
    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] != ' ':
            return board[0][col]

    # Check diagonals
    if board[0][0] == board[1][1] == board[2][2] != ' ':
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != ' ':
        return board[0][2]

    # If no winning combination is found, return None
    return None


# Step 6: Play the Game
def play_game():
    print("Welcome to Tic-Tac-Toe!")
    print("Player 1: X | Player 2: O")
    print_board()

    current_player = 'X'
    while True:
        print("Player", current_player, "'s turn.")
        row, col = get_move(current_player)
        make_move(current_player, row, col)
        print_board()

        winner = check_winner()
        if winner:
            print("Player", winner, "wins!")
            break

        if all(board[i][j] != ' ' for i in range(3) for j in range(3)):
            print("It's a tie!")
            break

        current_player = 'O' if current_player == 'X' else 'X'


# Step 7: Start the Game
play_game()
