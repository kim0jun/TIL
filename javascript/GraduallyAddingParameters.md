last chair
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

이번 문제는 숫자를 차례대로 전부 더하는 것이다 .

모든 arguments의 합을 반화하는 add라는 function을 만들어라. 
어때 쉽지? 안그래?

그러면 한번 꽈줄께, 파라메터를 넣을때마다 그 위치에 참조해 값이 점차 증가하도록 만들어라

```javascript
    add(3,4,5); 
    /*
    returns ( 3 * 1 ) + ( 4 * 2 ) + ( 5 * 3 ) = 26
    */

```

function은 arguments가 없을때 0을 반환다는것을 기억해라 arguments


```javascript

    add(); //=> 0
    add(1,2,3); //=> 14
    add(1,4,-5,5); //=> 14

```







##my solution

-  쉽다. arguments.lenght을 이용해서 반복문을 실행하고 최종값을 반환하면된다.
-  it's easily

```function add() {
        var total = 0
        //arguments는 array가아니라 object형식이라서 reduce를 사용할수없다. for문을이용하자
        for(var i=0 ; i<arguments.length;i++){
            total += arguments[i]*(i+1)
        }
        //최종값 반환 
        return total
    }  
   
```




##other solution

- reduce.call 사용할수있구나... 다음번에는 나도 이렇게한번사용해봐야겠다. 

```
function add() {
        return [].reduce.call(arguments, function(sum,v,i) { return sum + v * (i+1); }, 0);
    }
```



