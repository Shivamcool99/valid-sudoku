# valid-sudoku
class Solution {
    public boolean isValidSudoku(char[][] board) {
        if (board == null || board.length != 9 || board[0].length != 9)
            return false; // Check if the board is null or not 9x9

        // Check rows
        for (int row = 0; row < 9; row++) {
            if (!isValidRow(board, row)) {
                return false;
            }
        }

        // Check columns
        for (int col = 0; col < 9; col++) {
            if (!isValidColumn(board, col)) {
                return false;
            }
        }

        // Check 3x3 sub-boxes
        for (int row = 0; row < 9; row += 3) {
            for (int col = 0; col < 9; col += 3) {
                if (!isValidSubBox(board, row, col)) {
                    return false;
                }
            }
        }

        return true; // If all rows, columns, and sub-boxes are valid, return true
    }

    private boolean isValidRow(char[][] board, int row) {
        boolean[] seen = new boolean[10];
        for (int col = 0; col < 9; col++) {
            char digit = board[row][col];
            if (digit != '.') {
                int num = digit - '0';
                if (seen[num]) {
                    return false;
                }
                seen[num] = true;
            }
        }
        return true;
    }

    private boolean isValidColumn(char[][] board, int col) {
        boolean[] seen = new boolean[10];
        for (int row = 0; row < 9; row++) {
            char digit = board[row][col];
            if (digit != '.') {
                int num = digit - '0';
                if (seen[num]) {
                    return false;
                }
                seen[num] = true;
            }
        }
        return true;
    }

    private boolean isValidSubBox(char[][] board, int startRow, int startCol) {
        boolean[] seen = new boolean[10];
        for (int row = startRow; row < startRow + 3; row++) {
            for (int col = startCol; col < startCol + 3; col++) {
                char digit = board[row][col];
                if (digit != '.') {
                    int num = digit - '0';
                    if (seen[num]) {
                        return false;
                    }
                    seen[num] = true;
                }
            }
        }
        return true;
    }
}

