#include <iostream>
#include <limits> // For numeric_limits
using namespace std;

const int SIZE = 3;
char board[SIZE][SIZE];

// Function declarations
void initializeBoard();
void printBoard();
bool checkWin(char player);
bool checkDraw();

int main() {
    initializeBoard();
    char currentPlayer = 'X';
    int row, col;
    
    cout << "Welcome to Tic-Tac-Toe Game!\n";
    printBoard();
    
    while (true) {
        cout << "Player " << currentPlayer << ", enter row and column (0-2): ";
        
        if (!(cin >> row >> col)) {
            cout << "Invalid input. Please enter numbers only.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            continue;
        }
        
        if (row<0 ||  row>=SIZE ||  col<0 || col>=SIZE) {
            cout<<"Position out of bounds. Please enter values between 0-2.\n";
            continue;
        }
        
        if (board[row][col] != ' ') {
            cout << "That space is already taken. Try again.\n";
            continue;
        }
        
        board[row][col] = currentPlayer;
        printBoard();
        
        if (checkWin(currentPlayer)) {
            cout << "Player " << currentPlayer << " wins!\n";
            break;
        }
        
        if (checkDraw()) {
            cout << "It's a draw!\n";
            break;
        }
        
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }
    
    return 0;
}

// Function definitions
void initializeBoard() {
    for (int i = 0; i < SIZE; ++i)
        for (int j = 0; j < SIZE; ++j)
            board[i][j] = ' ';
}

void printBoard() {
    cout << "\n";
    for (int i = 0; i < SIZE; ++i) {
        cout << " ";
        for (int j = 0; j < SIZE; ++j) {
            cout << board[i][j];
            if (j < SIZE - 1) cout << " | ";
        }
        cout << "\n";
        if (i < SIZE - 1)
            cout << "---+---+---\n";
    }
    cout << "\n";
}

bool checkWin(char player) {
    // Check rows and columns
    for (int i = 0; i < SIZE; ++i) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player))
            return true;
    }
    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player))
        return true;
    return false;
}

bool checkDraw() {
    for (int i = 0; i < SIZE; ++i)
        for (int j = 0; j < SIZE; ++j)
            if (board[i][j] == ' ')
                return false;
    return true;
}

       
