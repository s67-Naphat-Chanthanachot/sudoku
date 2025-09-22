int[][] board = {
{5,3,0, 0,7,0, 0,0,0},
{6,0,0, 1,9,5, 0,0,0},
{2,1,0, 6,2,7, 1,5,2},
{7,0,2, 1,5,2, 5,0,2},
{8,2,6, 0,2,1, 7,2,6},
{5,1,0, 5,0,1, 5,2,3},
{9,0,4, 0,7,3, 0,0,6},
{8,2,6, 6,1,8, 0,0,0},
{6,2,7, 9,1,6, 8,0,0}
}; 
int sizeCell =67;
void setup() {
  size(600,600);
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
        fill(0);
        text(board[i][j], j*sizeCell + sizeCell/2, i*sizeCell + sizeCell/2);
      }
      j++;
    }
    i++;
  }
}
void draw() {
  background(255);
  drawNumbers();
  drawGrid();
}
