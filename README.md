# Tic-Tac-Toe
This is the game which i have made by using C++ language code.

#include <iostream>
using namespace std;

// Initializing the board
char board[3][3] = {{'1', '2', '3'}, {'4', '5', '6'}, {'7', '8', '9'}};
char currentPlayer = 'X'; // Player 1 starts
int choice;
int row, col;

// Function to display the board
void displayBoard() {
    cout << "\nTic Tac Toe Game\n";
    cout << "Player 1 (X) - Player 2 (O)\n\n";
    
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << " " << board[i][j] << " ";
            if (j < 2) cout << "|";
        }
        cout << endl;
        if (i < 2) cout << "---|---|---" << endl;
    }
}

// Function to make a move
void makeMove() {
    cout << "Player " << currentPlayer << "'s turn. Enter a number (1-9): ";
    cin >> choice;

    switch(choice) {
        case 1: row = 0; col = 0; break;
        case 2: row = 0; col = 1; break;
        case 3: row = 0; col = 2; break;
        case 4: row = 1; col = 0; break;
        case 5: row = 1; col = 1; break;
        case 6: row = 1; col = 2; break;
        case 7: row = 2; col = 0; break;
        case 8: row = 2; col = 1; break;
        case 9: row = 2; col = 2; break;
        default: cout << "Invalid move! Try again.\n"; makeMove(); return;
    }

    // Check if the cell is already filled
    if (board[row][col] == 'X' || board[row][col] == 'O') {
        cout << "Cell already filled! Try again.\n";
        makeMove();
    } else {
        board[row][col] = currentPlayer;
    }
}

// Function to check if a player has won
bool checkWin() {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) return true;
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) return true;
    }
    
    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) return true;
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) return true;

    return false;
}

// Function to check if the game is a draw
bool checkDraw() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] != 'X' && board[i][j] != 'O') return false;
        }
    }
    return true;
}

int main() {
    while (true) {
        displayBoard();
        makeMove();

        if (checkWin()) {
            displayBoard();
            cout << "Player " << currentPlayer << " wins!\n";
            break;
        }

        if (checkDraw()) {
            displayBoard();
            cout << "It's a draw!\n";
            break;
        }

        // Switch the player
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }
    return 0;
}

