## 36	Valid Sudoku

Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

## Solution

纯模拟
```C++
class Solution {
private:
    bool marked[10];
    void clearMark(){
        fill_n(&marked[0], 10, false);
    }
    bool isLineValid(vector<char> line){
        clearMark();
        for(int i=0; i<9; i++){
            if(line[i] == '.') continue;
            int d = line[i] - '0';
            if(marked[d]) return false;
            marked[d] = true;
        }
        return true;
    }
    bool areColumnsValid(vector<vector<char>>& board){
        for(int i=0; i<9; i++){
            clearMark();
            for(int j=0; j<9; j++){
                if(board[j][i] == '.') continue;
                int d = board[j][i] - '0';
                if(marked[d]) return false;
                marked[d] = true;
            }
        }
        return true;
    }
    bool isSubBoxValid(vector<vector<char>> &board, int r, int c){
        clearMark();
        for(int i = r; i<r+3; i++){
            for(int j=c; j<c+3; j++){
                if(board[i][j] == '.') continue;
                int d = board[i][j] - '0';
                if(marked[d]) return false;
                marked[d] = true;
            }
        }
        return true;
    }
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        for(int i=0; i<board.size(); i++){
            if(!isLineValid(board[i])) return false;
        }
        if(!areColumnsValid(board)) return false;
        for(int i=0; i<9; i+=3){
            for(int j=0; j<9; j+=3){
                if(!isSubBoxValid(board, i, j)) return false;
            }
        }
        return true;
    }
};
```