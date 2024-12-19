#include <iostream>
#include <stdlib.h>
using namespace std;

// Array for the board
char board[3][3] = {{'1','2','3'},{'4','5','6'},{'7','8','9'}};

// Variable Declaration
int choice;
int row, column;
char turn = 'X';
bool draw = false;

// Function to show the current status of the gaming board
void display_board() {
    // Render Game Board Layout
    cout << "PLAYER - 1 [X]\t PLAYER - 2 [O]\n\n";
    cout << "\t     |     |     \n";
    cout << "\t  " << board[0][0] << "  |  " << board[0][1] << "  |  " << board[0][2] << "  \n";
    cout << "\t_____|_____|_____\n";
    cout << "\t     |     |     \n";
    cout << "\t  " << board[1][0] << "  |  " << board[1][1] << "  |  " << board[1][2] << "  \n";
    cout << "\t_____|_____|_____\n";
    cout << "\t     |     |     \n";
    cout << "\t  " << board[2][0] << "  |  " << board[2][1] << "  |  " << board[2][2] << "  \n";
    cout << "\t     |     |     \n";
}

// Function to get the player input and update the board
void player_turn() {
    if (turn == 'X') {
        cout << "\nPlayer - 1 [X] turn: ";
    } else if (turn == 'O') {
        cout << "\nPlayer - 2 [O] turn: ";
    }

    // Taking input from the user
    cin >> choice;

    // Switch case to determine the row and column based on choice
    switch (choice) {
        case 1: row = 0; column = 0; break;
        case 2: row = 0; column = 1; break;
        case 3: row = 0; column = 2; break;
        case 4: row = 1; column = 0; break;
        case 5: row = 1; column = 1; break;
        case 6: row = 1; column = 2; break;
        case 7: row = 2; column = 0; break;
        case 8: row = 2; column = 1; break;
        case 9: row = 2; column = 2; break;
        default:
            cout << "Invalid Move!\n";
            player_turn();
            return;
    }

    // Check if the selected cell is empty
    if (board[row][column] != 'X' && board[row][column] != 'O') {
        board[row][column] = turn;
        turn = (turn == 'X') ? 'O' : 'X';
    } else {
        cout << "Box already filled! Please choose another!!\n\n";
        player_turn();
    }

    display_board();
}

// Function to check the game status (Win, Draw, or Continue)
bool gameover() {
    // Check rows and columns for a win
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][0] == board[i][2]) return false;
        if (board[0][i] == board[1][i] && board[0][i] == board[2][i]) return false;
    }

    // Check diagonals for a win
    if (board[0][0] == board[1][1] && board[0][0] == board[2][2]) return false;
    if (board[0][2] == board[1][1] && board[0][2] == board[2][0]) return false;

    // Check if any cells are still empty
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] != 'X' && board[i][j] != 'O') return true;
        }
    }

    // If no empty cells, it's a draw
    draw = true;
    return false;
}

// Main function
int main() {
    cout << "\t\tT I C K -- T A C -- T O E -- G A M E\n";
    cout << "\t\tFOR 2 PLAYERS\n\n";

    while (gameover()) {
        display_board();
        player_turn();
    }

    if (!draw) {
        if (turn == 'O') {
            cout << "\nCongratulations! Player with 'X' has won the game!\n";
        } else {
            cout << "\nCongratulations! Player with 'O' has won the game!\n";
        }
    } else {
        cout << "\nGAME DRAW!!!\n";
    }

    return 0;
}
