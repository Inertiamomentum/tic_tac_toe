# tic_tac_toe
Tic Tac Toe game implemented in C
#include <stdio.h>

// Global variables
char board[3][3] = {
    {'1', '2', '3'},
    {'4', '5', '6'},
    {'7', '8', '9'}
};
int currentPlayer = 1;
char mark;

// Function prototypes
void displayBoard();
int checkWinner();
void makeMove();

// Main function
int main() {
    int gameStatus = 0;

    printf("Tic Tac Toe Game\n");
    printf("Player 1 (X)  -  Player 2 (O)\n\n");

    // Game loop
    while (gameStatus == 0) {
        displayBoard();
        makeMove();

        // Check if there's a winner or a draw
        gameStatus = checkWinner();
        currentPlayer = (currentPlayer % 2) + 1;
    }

    displayBoard();
    if (gameStatus == 1) {
        printf("==> Player %d wins!\n", (currentPlayer % 2) + 1);
    } else {
        printf("==> It's a draw!\n");
    }

    return 0;
}

// Display the Tic Tac Toe board
void displayBoard() {
    printf("\n");
    printf("     |     |     \n");
    printf("  %c  |  %c  |  %c  \n", board[0][0], board[0][1], board[0][2]);
    printf("_____|_____|_____\n");
    printf("     |     |     \n");
    printf("  %c  |  %c  |  %c  \n", board[1][0], board[1][1], board[1][2]);
    printf("_____|_____|_____\n");
    printf("     |     |     \n");
    printf("  %c  |  %c  |  %c  \n", board[2][0], board[2][1], board[2][2]);
    printf("     |     |     \n\n");
}

// Handle a player's move
void makeMove() {
    int choice;
    int row, column;

    printf("Player %d, enter your choice: ", currentPlayer);
    scanf("%d", &choice);

    // Map choice to board coordinates
    row = (choice - 1) / 3;
    column = (choice - 1) % 3;

    // Validate the move
    if (choice < 1 || choice > 9 || board[row][column] == 'X' || board[row][column] == 'O') {
        printf("Invalid move. Try again.\n");
        makeMove();
    } else {
        mark = (currentPlayer == 1) ? 'X' : 'O';
        board[row][column] = mark;
    }
}

// Check the game status
int checkWinner() {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) return 1;
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) return 1;
    }

    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) return 1;
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) return 1;

    // Check for a draw
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] != 'X' && board[i][j] != 'O') return 0;
        }
    }

    return -1;  // Draw
}
