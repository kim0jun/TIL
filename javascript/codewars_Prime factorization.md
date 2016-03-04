Prime factorization
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

주어진 값을 소수로 인수분해 하여 오브젝트 형태로 반환하는 함수를 만들어라.

24에 대한 상수인수분해의 경우  (2^3) * (3^1) 와 같다.

상수 라이브러리를 사용하지말고.  1보다 큰 정수를 취했을을때 그리고 factor라는 함수를 호출했을때 나누어진 상수와 해당상수가 몇번반복했는지 반환하는 PrimeFactorizer 라는 함수를 작성하여라




###작업내용


```

new PrimeFactorizer(24).factor 
//should return { '2': 3, '3': 1 }
    

```



##my solution

- 반복문을 이용하여 주어진값을 계속해서 나눈다 
- 만약 해당값으로 정확히나누어진다면 해당값을 반환할 오브젝트에담고 다시한번나눈다.
- 만약 해당값으로 나누어지지않는다면 해당값보다 하나큰 숫자를이용해서 나눈다.
- 해당값이 1로 나누어 질때 까지 반복한다.


```javascript

    function PrimeFactorizer(n){
        var returnObj = {}
        for(var i = 2; n != 1;i){
            if(n%i == 0){
                n = n/i
                returnObj[i] = ++returnObj[i] || 1
            }
            else               i++
        }	

        return {
            factor:returnObj
        }
    }

   
```




##other solution

- 방법에 대한 것 은 나와 동일한데 코드를 보기가 훨신 쉽게되었다.
- while문을 사용해서 깔끔하고 가독성 높은 코드를 작성하였다.
- 연산과정도 나보다 짧을것으로 예상된다.
- 그리고 연산식을 사용할때 === 을 잘사용해봐야겠다. ==의 경우에는 피연산자의 타입이 강제로 바뀌어서 0 == false의 결과값이 true로 출력된다.


```javascript

    function PrimeFactorizer(n) {
        var i, factors = {};
        for (i=2; i <= n; i++) {
            while (n%i === 0) {
                factors[i] = 1 + (factors[i]||0); n /= i;
            }
        }
        return {factor:factors};
    }

```


- 다른방법들은 코드 가독성도 떨어지고 효율적이지 않다.
- 그래도 상수 도출하는 알고리즘은 쓸만한것같다.


```javascript
    function leastFactor(n) {
        if (n==0) return 0;  
        if (n%1 || n*n<2) return 1;
        if (n%2==0) return 2;  
        if (n%3==0) return 3;  
        if (n%5==0) return 5;  
        var m = Math.sqrt(n);
        for (var i=7;i<=m;i+=30) {
            if (n%i==0)      return i;
            if (n%(i+4)==0)  return i+4;
            if (n%(i+6)==0)  return i+6;
            if (n%(i+10)==0) return i+10;
            if (n%(i+12)==0) return i+12;
            if (n%(i+16)==0) return i+16;
            if (n%(i+22)==0) return i+22;
            if (n%(i+24)==0) return i+24;
        }
        return n
    }
```



