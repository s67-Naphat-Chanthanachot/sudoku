int[][] board = new int[9][9]; 
boolean[][] fixed = new boolean[9][9]; 
int sizeCell = 60;
int r = -1, c = -1;           

void setup() {
  size(500, 500);
  loadGame("sudoku.txt"); 
}

void draw() {
  background(255);
  drawGrid();
}

void drawGrid() {
  int i = 0;
  while (i <= 9) {
    strokeWeight((i % 3 == 0) ? 3 : 1);
    line(i*sizeCell, 0, i*sizeCell, height);
    line(0, i*sizeCell, width, i*sizeCell);
    i++;
  }
}

void loadGame(String fileName) {
  String[] lines = loadStrings(fileName);
  int i = 0;
  int row = 0;
  while (i < lines.length && row < 9) {
    String line = trim(lines[i]);
    if (line.length() > 0) {
      String[] nums = splitTokens(line, " \t");
      int j = 0;
      while (j < 9 && j < nums.length) {
        board[row][j] = int(nums[j]);
        fixed[row][j] = (board[row][j] != 0);
        j++;
      }
      row++;
    }
    i++;
  }
}
