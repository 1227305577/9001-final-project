def print_board(board: list):
    for row in board:
        line = ''
        for piece in row:
            if piece == 0:
                line += '+'
            if piece == 1:
                line += '★'
            if piece == 2:
                line += '☆'
        print(line)


def drop_piece(board, col):
    row = len(board)
    for i in range(row - 1, -1, -1):
        if board[i][col] == 0:
            return i
        else:
            print(f'[row{row - i},column{col + 1}]is full,your piece is supported by it')
    return -1


def check_win(board, row, col, piece):
    directions = [
        (0, 1),
        (1, 0),
        (1, 1),
        (1, -1)
    ]
    rows = len(board)
    cols = len(board[0])
    for dr, dc in directions:
        count = 1
        r = row + dr
        c = col + dc
        while 0 <= r < rows and 0 <= c < cols and board[r][c] == piece:
            count += 1
            r += dr
            c += dc

        r = row - dr
        c = col - dc
        while 0 <= r < rows and 0 <= c < cols and board[r][c] == piece:
            count += 1
            r -= dr
            c -= dc

        if count >= 5:
            return True

    return False


board = [[0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
         ]
win = False
turn = 0
user1 = input("Hello user1. What's your name:")
user2 = input("Hello user2. What's your name:")
cols = len(board[0])
while win == False:
    if 0 not in board[0] and 0 not in board[0] and 0 not in board[1] and 0 not in board[2] and 0 not in board[
        3] and 0 not in board[4] and 0 not in board[5] and 0 not in board[6]:
        print(f'board is full,{user1} and {user2} reached a draw.')
        break
    print_board(board)
    turn += 1
    if turn % 2 == 1:
        step = 'none'
        while step != 'ok':
            column = int(input(f'{user1},which column is your choice:'))
            col = column - 1
            if col < 0 or col >= cols:
                print(f'Column out of range. Try again.')
                continue
            row = drop_piece(board, col)
            if row == -1:
                print(f'This column is full. Try again.')
                continue
            board[row][col] = 1
            if check_win(board, row, col, 1):
                print_board(board)
                print(f"{user1} wins!")
                win = True
                break
            step = 'ok'
    else:
        step = 'none'
        while step != 'ok':
            column = int(input(f'{user2},which column is your choice:'))
            col = column - 1
            if col < 0 or col >= cols:
                print(f'Column out of range. Try again.')
                continue
            row = drop_piece(board, col)
            if row == -1:
                print(f'This column is full. Try again.')
                continue
            board[row][col] = 2
            if check_win(board, row, col, 2):
                print_board(board)
                print(f"{user2} wins!")
                win = True
                break
            step = 'ok'
