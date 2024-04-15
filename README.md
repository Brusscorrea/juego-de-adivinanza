# juego-de-adivinanza
import random

def generate_board(rows, cols):
    # Genera una matriz de números aleatorios y letras como tablero
    letters = ['a', 'b', 'c']
    board = [[random.choice([random.randint(1, 10)] + letters) for _ in range(cols)] for _ in range(rows)]
    return board

def show_board(board):
    # Muestra el tablero al jugador, ocultando el valor secreto con un asterisco
    for row in board:
        print(' '.join(str(x) if isinstance(x, int) else x for x in row))

def hide_value(board):
    # Oculta un valor secreto en el tablero con un asterisco
    secret_row = random.randint(0, len(board) - 1)
    secret_col = random.randint(0, len(board[0]) - 1)
    secret_value = board[secret_row][secret_col]
    board[secret_row][secret_col] = '*'
    return secret_value, board

def play_game(rows, cols):
    # Juega el juego de adivinanzas
    board = generate_board(rows, cols)
    secret_value, hidden_board = hide_value(board)
    show_board(hidden_board)
    guess = input("Adivina el valor secreto: ")
    if str(guess).lower() == str(secret_value).lower():
        print("¡Correcto!")
    else:
        print("Incorrecto, el valor era:", secret_value)

def main():
    print("Bienvenido al juego ")
    size = input("Tamaño del tablero : ")
    rows, cols = map(int, size.split('x'))
    play_game(rows, cols)
    while True:
        play_again = input("¿Quieres jugar de nuevo? (s/n): ").lower()
        if play_again != 's':
            break
        play_game(rows, cols)

if __name__ == "__main__":
    main()
