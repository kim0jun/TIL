Unique In Order
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

2d 배열과 세대의 배열을 건내주면, Conway's Game of Life에 의해 n 번째 타임스텝을 계산하여라.

규칙은 다음과 같다.
1. 살아있는 셀은 2보다 작은 셀과 함께있으면죽는다. 
2. 살아있는셀은 3개보다 많은 살아있는 셀과 교접하면 죽는다.
3. 살아있는셀은  2또는 3개의 살아있는셀과 인접해있으면 다음세대에도 생존하다.
4. 죽은셀은 3개의 살아있는 셀을 만나면 살아난다.

각각의 셀들은 8개의 이웃으로 직접 둘러쌓여있다. 세계는 무한의 x,y로 이루어져있다.(무한의 x,y에서 주어진 2d배열의 모습을 찾아야함)




###작업내용
 




##my solution


- 주변의 살아있는 셀을구하는 함수를 이용해서 if문을 이용해서 다음세대의 셀을 만들자 
- 3*3 안의 픽셀이아니라 무한한 맵에서 오브젝트의 변화를 반환해야함으로 코드수정해야함

```javascript

function nextGen(cells){
  // Uncomment next row to have an example
  // return cells;
  let nextCells = [];
  
  cells.forEach((row,i)=>{    
    let nextRow = [];
    row.forEach((cell,j)=>{
      //cell 이 1 이면 live 아니면 dead
      const liveNeighbourCount = checkNeighbour(cells,i,j);
      let newCell = 0;
      if (cell === 1){
        //셀이 살아있을때
        if(liveNeighbourCount === 2  || liveNeighbourCount === 3)  newCell = 1;
        else newCell = 0;
      
      } else {
        //셀이 죽었을때
        if(liveNeighbourCount === 3 )  newCell = 1;
        else newCell = 0;
      
      }
         
      nextRow.push(newCell)
      
    })
    nextCells.push(nextRow)
  })
  
  return nextCells
}


function checkNeighbour(cells,row,column){
    var neighbourCount = 0 
        for (var i = -1; i < 2; i += 1){
            for (var n = -1; n < 2; n += 1){
            if(row+i>=0 && row+i<cells.length && column+n>=0 && column+n<cells[0].length&&( i != 0 || n != 0)){
                neighbourCount += cells[row+i][column+n] 
            } 
        }
    }
    return neighbourCount 
}
```




##other solution
    직관적으로 잘짯다. array의 map함수를 잘활용하였다.
    반복문을 최소화 하여 가독성이높고, 코드도 가독성높게 정리하였다.

```javascript
    function nextGen(cells) {
        var get = function (i, j) { return (cells[i] && cells[i][j]) | 0 };
        
        cells = cells.map(function (row, i) {
            return row.map(function (alive, j) {
            var neighbors =
                get(i-1, j-1) + get(i-1, j) + get(i-1, j+1) +
                get(i  , j-1)               + get(i  , j+1) +
                get(i+1, j-1) + get(i+1, j) + get(i+1, j+1);
                
            return (neighbors === 3 || (neighbors === 2 && alive)) | 0;
            });
        });
        
        return cells;
    }
  

```