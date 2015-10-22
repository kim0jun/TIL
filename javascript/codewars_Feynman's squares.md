Feynman's squares
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

(오늘은 시간이없어서 번역은 생략)

nxn으로 이루어진 타일로 만들수있는 정사각형의 갯수를 구한다. 이 때 위치가 다르면 다른정사각형으로간주



###작업내용
 

```
countSquares(1) =  1
countSquares(2) =  5
countSquares(3) = 14

```



##my solution

- n에서 구할수있는 정사각형의 수는  countSquares(n-1)+n*n 이다.
- 반복문을 이용해서 구현

```javascript
    
    function countSquares(n){
        var totalCount = 0
        for(i=1;i<=n;i++){
            totalCount += i*i
        }
        return totalCount
    }

   
```




##other solution

- 반복문을 이용허지않은 알고리즘을 이용하였다.
- n(n+1)(2n+1)/6 는 1~n까지의 합이라고한다.


```javascript

    function countSquares(n){
        return n*(n+1)*(2*n+1)/6
    }

```

- 나와같은 알고리즘을 이용해서 구현
- 재귀함수를 이용하여 가독성도,효율성도 내 코드보다 높은 것 같다.
- 다음번에는 재귀함수를 이용해서 코드를 짜봐야겠다.

```javascript
    function countSquares(n){
        return n == 1 ? 1 : (n * n) + countSquares(--n);
    }
```javascript
