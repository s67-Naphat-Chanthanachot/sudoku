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
  drawNumbers();
  highlightSelected();
}

void mousePressed() {
  int rr = constrain(mouseY / sizeCell, 0, 8);
  int cc = constrain(mouseX / sizeCell, 0, 8);
  r = rr;
  c = cc;
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

void drawNumbers() {
  textAlign(CENTER, CENTER);
  textSize(24);
  int i = 0;
  while (i < 9) {
    int j = 0;
    while (j < 9) {
      if (board[i][j] != 0) {
        if (fixed[i][j]) {
          fill(0); 
        } else {
          fill(0, 102, 204); 
        }
        text(board[i][j], j*sizeCell + sizeCell/2, i*sizeCell + sizeCell/2);
      }
      j++;
    }
    i++;
  }
}

void highlightSelected() {
  if (r != -1 && c != -1) {
    noFill();
    stroke(255, 0, 0);
    strokeWeight(3);
    rect(c*sizeCell, r*sizeCell, sizeCell, sizeCell);
  }
}

boolean checkValid(int row, int col, int val) {
  int i = 0;
  while (i < 9) {
    if (board[row][i] == val) return false; 
    if (board[i][col] == val) return false; 
    i++;
  }

  int startR = (row / 3) * 3;
  int startC = (col / 3) * 3;
  i = 0;
  while (i < 3) {
    int j = 0;
    while (j < 3) {
      if (board[startR + i][startC + j] == val) return false; 
      j++;
    }
    i++;
  }
  return true;
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
