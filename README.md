void draw() {
  background(255);
  drawGrid();
  drawNumbers();
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
