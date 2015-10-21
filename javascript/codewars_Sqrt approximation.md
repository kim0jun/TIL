Sqrt approximation
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

우리는 `sqrt`함수와 거의 비슷하기를 원한다. 보통 이 함수는 부동 소수점 수를 취하고
다른 부동소수점 수를 반환한다. 그러나 이번 문제는 대신에 정수형 수를 사용한다.

당신의 과제는 정수를 취하고 어떤 정수를 반환하는 함수를 만드는것이다. 

- 정수 `k`는 `n`이 재곱수 이고 `k*k == n`  일때 반환된다.

- 공간 `(k, k+1)`은 , `k*k < n` 그리고 `n < (k+1) * (k+1)` 일때 반환된다.



###작업내용
 

```
Test.assertEqual  (sqrtApproximation(4), 2);
Test.assertSimilar(sqrtApproximation(5), [2, 3]));

```



##my solution

- 단순하게 풀었다. 먼저 만약 0이면 0을 반환한다
- 그리고 정수형임으로 0~파라메터값-1 까지 반복문을 돌린다.
- 매 루프마다 1번 혹은 2번 제약을 확인하고 만약 맞다면 해당값을 반환한다.


```javascript

    function sqrtApproximation(number) {
        if(number == 0) return 0
        for(var k = 0;k < number,k++){
            if(k*k == number)                                return k
            else if(k*k < number  && number < (k+1) * (k+1)) return [k,k+1]
        }  
    }
   
```




##other solution

- 불필요한 반복을 줄였다. for문을 이런식으로는 한번도 안 사용해봤는데 내가 너무 단순하게 생각한것같다.
- number >= i*i를이용하여 number의 제곱혹은 제곱 이전까지만 반복해서 만약 재곱이면 재곱근을 반환하고
- 만약 재곱근이아니라면 공간정보를 담은 배열을 반환한다.



```javascript

    function sqrtApproximation(number) {
        for (var i = 0; number >= i*i; i++) if (i*i === number) return i
        return [i - 1, i]
    }
}    

