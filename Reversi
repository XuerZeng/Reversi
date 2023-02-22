void printBoard(char board[][26], int n) {
  printf("  ");
  for(int i = 0;i<n;i++){
    printf("%c",97+i);
  }
  printf("\n");
  for(int j = 0;j<n;j++){
    printf("%c ",97+j);
    for(int k = 0; k<n;k++){
      printf("%c",board[j][k]);
    }
    printf("\n");
  }
}

bool positionInBounds(int n, int row, int col) {
  bool inBound;
  if(row>=0&&row<n&&col>=0&&col<n){
    inBound = true;
  }else{
    inBound = false;
  }
  return inBound;

}
int nextNum (char board[][26],int n, char tile, int row, int col){
  char tempBoard[26][26];
  
  for (int i=0;i<n;i++){
    for (int j=0;j<n;j++){
      tempBoard[i][j]=board[i][j];
    }
  }
  validAndFlip(tempBoard,n,tile,row+97,col+97);
  int xDir[]= {1,1,0,-1,-1,-1,0,1};
  int yDir[]={0,-1,-1,-1,0,1,1,1};
  bool done = false;
  int count = 0;
  for (int i=0;i<n;i++){
    for (int j=0;j<n;j++){
      if (tempBoard[i][j]=='U'){
        for (int k=0;k<8&&!done;k++){
          if(checkLegalInDirection(tempBoard,n,i,j,tile,xDir[k],yDir[k])&&!done){
            count++;
            done = true;
          }
        }
      }
    }
  }
  return count;
}

int score (char board[][26],int n,char tile, int row, int col){
  int xDir[]= {1,1,0,-1,-1,-1,0,1};
  int yDir[]={0,-1,-1,-1,0,1,1,1};
  int score=0;
  for(int i=0;i<8;i++){
    int rowDir = xDir[i];
    int colDir = yDir[i];
    int rowAdd = row+rowDir;
    int colAdd = col+colDir;
    if (checkLegalInDirection(board,n,row,col,tile,rowDir,colDir)){
      while (board[rowAdd][colAdd]!=tile&&board[rowAdd][colAdd]!='U'){
        score++;
        rowAdd+=rowDir;
        colAdd+=colDir;
      }
    }
  }
  return score;
}

int middleNum (char board[][26],int n, char tile,int row, int col){
  char tempBoard[26][26];
  for (int i=0;i<n;i++){
    for (int j=0;j<n;j++){
      tempBoard[i][j]=board[i][j];
    }
  }
  validAndFlip(tempBoard,n,tile,row+97,col+97);
  int count;
  for (int i=1;i>-1;i--){
    for (int j=1;j>-1;j--){
      if (tempBoard[n/2-i][n/2-j]==tile){
        count ++;
      }
    }
  }
  return count;
}

void validAndFlip (char board[][26],int n,char tile, char row, char col){
  bool valid=false;
  int deltaRow,deltaCol;
  int rowDir,colDir;
  int rowNum,colNum;
  bool done = false;
  rowNum=row-'a';
  colNum=col-'a';
  int xDir[]={1,1,0,-1,-1,-1,0,1};
  int yDir[]={0,-1,-1,-1,0,1,1,1};
  bool finalValid = false;
  for(int i=0;i<8;i++){
    if(checkLegalInDirection(board,n,rowNum,colNum,tile,xDir[i],yDir[i])){;
      deltaRow = xDir[i];
      deltaCol = yDir[i];
      valid = true;
      finalValid = true;
    }
  
    rowDir = rowNum+deltaRow;
    colDir = colNum+deltaCol;
    int time = 2;
    if (valid){
      board[rowNum][colNum]=tile;
      for(int i=rowNum;positionInBounds(n,rowDir,colDir)&&!done;i++){
        for(int j = colNum;positionInBounds(n,rowDir,colDir)&&!done;j++){
          if(board[rowDir][colDir]!=tile&&board[rowDir][colDir]!='U'){
            board[rowDir][colDir]=tile;
            rowDir = rowNum+deltaRow*time;
            colDir = colNum+deltaCol*time;
            time++;
            done = false;
          }else{
            done = true;
          }
        }
      }
    }
    done = false;
    valid = false;
  }

}

bool checkLegalInDirection(char board[][26], int n, int row, int col,
                         char colour, int deltaRow, int deltaCol) {
  int rowMove,colMove;
  rowMove = row+deltaRow;
  colMove = col+deltaCol;
  bool done = false;
  int state =1;
  bool legal;
  if(colour=='W'){
    for(int i =1;positionInBounds(n,rowMove,colMove)&&!done;i++){
      if(board[rowMove][colMove]=='B'){
        state = 2;
        done = false;
      }else if(board[rowMove][colMove]=='U'){
        state=1;
        done = true;
      }
      if(board[rowMove][colMove]=='W'&&state==2){
        state = 3;
        done = true;
      }else if(board[rowMove][colMove]=='W'&&state!=2){
        state = 1;
        done = true;
      }
      rowMove = row+deltaRow*(i+1);
      colMove = col+deltaCol*(i+1);
    }
  }else if(colour=='B'){
    for(int i =1;positionInBounds(n,rowMove,colMove)&&!done;i++){
      if(board[rowMove][colMove]=='W'){
        state = 2;
        done = false;
      }else if(board[rowMove][colMove]=='U'){
        state=1;
        done = true;
      }
      if(board[rowMove][colMove]=='B'&&state==2){
        state = 3;
        done = true;
      }else if(board[rowMove][colMove]=='B'&&state!=2){
        state = 1;
        done = true;
      }
      rowMove = row+deltaRow*(i+1);
      colMove = col+deltaCol*(i+1);
    }
  }
  if(state==3){
    legal = true;
  }else{
    legal = false;
    
  }
  return legal;
}
int opponentMove(char board[][26], int n, char tile, int row, int col){
  char tempBoard[26][26];
  for (int i=0;i<n;i++){
    for (int j=0;j<n;j++){
      tempBoard[i][j]=board[i][j];
    }
  }
  validAndFlip(tempBoard,n,tile,row+97,col+97);
  int xDir[]= {1,1,0,-1,-1,-1,0,1};
  int yDir[]={0,-1,-1,-1,0,1,1,1};
  bool done = false;
  int count = 0;
  for (int i=0;i<n;i++){
    for (int j=0;j<n;j++){
      if (tempBoard[i][j]=='U'){
        for (int k=0;k<8&&!done;k++){
          if(tile=='B'){
            if(checkLegalInDirection(tempBoard,n,i,j,'W',xDir[k],yDir[k])&&!done){
              count++;
              done = true;
            }
          }else if(tile=='W'){
            if(checkLegalInDirection(tempBoard,n,i,j,'B',xDir[k],yDir[k])&&!done){
              count++;
              done = true;
            }
          }
        }
      }
    }
  }
  return count; 
}
bool opponentAvaliable(char board[][26],int n, char tile,int row, int col){
  int xDir[]= {1,1,0,-1,-1,-1,0,1};
  int yDir[]={0,-1,-1,-1,0,1,1,1};
  char tempBoard[26][26];
  bool done = false;
  int count = 0;
  for (int i=0;i<n;i++){
    for (int j=0;j<n;j++){
      tempBoard[i][j]=board[i][j];
    }
  }
  validAndFlip(tempBoard,n,tile,row+97,col+97);
  bool go;
  for (int i=0;i<n;i++){
    for (int j=0;j<n;j++){
      if (tempBoard[i][j]=='U'){
        for (int k=0;k<8&&!done;k++){
          if(tile=='W'){
            if(checkLegalInDirection(board,n,i,j,'B',xDir[k],yDir[k])&&!done){         
              done = true;
              if((i==0&&j==0)||(i==(n-1)&&j==0)||(i==0&&j==(n-1))||(i==(n-1)&&j==(n-1))){
                go=false;
              }else{
                go = true;
              }
            }
          }else if(tile=='B'){
            if(checkLegalInDirection(board,n,i,j,'W',xDir[k],yDir[k])&&!done){        
              done = true;
              if((i==0&&j==0)||(i==(n-1)&&j==0)||(i==0&&j==(n-1))||(i==(n-1)&&j==(n-1))){
                go=false;
              }else{
                go = true;
              }
            }
          }
        }
        done = false;
      }
    }
  }
  
  return go;
}

int makeMove(const char board[][26], int n, char turn, int *row, int *col){
  int xDir[]= {1,1,0,-1,-1,-1,0,1};
  int yDir[]={0,-1,-1,-1,0,1,1,1};
  int tempRow, tempCol;
  bool done = false;
  int mark = 0,highest=0;
  int next = 0, user=0,largest=0,most=0,middle =0;
  int opponent = 0, least = 100;
  int mostMiddle;
  for (int i=0;i<n;i++){
    for (int j=0;j<n;j++){
      if (board[i][j]=='U'&&positionInBounds(n,i,j)){
        for (int k=0;k<8&&!done;k++){
          if(checkLegalInDirection(board,n,i,j,turn,xDir[k],yDir[k])&&!done){
            tempRow = i;
            tempCol = j;   
            done = true;
            if((tempRow==0&&tempCol==0)||(tempRow==(n-1)&&tempCol==0)||(tempRow==0&&tempCol==(n-1))||(tempRow==(n-1)&&tempCol==(n-1))){
              mark+=4;
              //printf("hhh");
            }
            next = nextNum(board,n,turn,tempRow,tempCol);
            user=score(board,n,turn,tempRow,tempCol);
            middle = middleNum(board,n,turn,tempRow,tempCol);
            opponent = opponentMove(board,n,turn,tempRow,tempCol);
            if(next>largest){
              largest=next;       
              next=0;
              mark+=2;
            }
            if(user>most){
              most = user;
              user=0;
              mark++;                        
            }
            if (middle>mostMiddle){
              mostMiddle = middle;
              middle=0;
              mark++;
            }
            if(opponentAvaliable(board,n,turn,tempRow,tempCol)){
              mark+=2;
              //printf("ddd");
            }
            if(opponent<least){
              least = opponent;
              opponent = 0;
              mark+=2;
            }
            if (mark>highest){
              highest=mark;
              mark = 0;
              *row = tempRow;
              *col = tempCol;
              
            }
          }
        }
      }
      done = false;
    }
  }
  //printBoard(board,n);
  return 0;
    
}
