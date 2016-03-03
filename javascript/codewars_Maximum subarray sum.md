Maximum subarray sum
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

배열,혹은 정수 리스트 에서 연속되는 값의 최대합의 값을구하라.





###작업내용


```

maxSequence([-2, 1, -3, 4, -1, 2, 1, -5, 4])
// should be 6: [4, -1, 2, 1]
    

```



##my solution

- 열속된 배열의 합이 최대로 나오려면 이전값과 현재값의 합이 0,c 보다 커야한다. 그렇지않을경우 최대값은 c이다
- 만약 두경우 모두 만족한다면 최대값을 갱신한다.
- 배열 전체에 걸쳐서 하기때문에 함수내 전역변수를 사용하여 최대값을 갱신하기전에 비교문을다시사용한다(비합리적) - Math.max 로 바꿀수있을 것 같다.


```javascript

    var maxSequence = function(arr){
        var maxValue = 0;
        arr.reduce(function(p,c,i,a){
            if(p+c < 0  || p+c < c){
                if(maxValue < c) maxValue = c;
                return c
            }else if(maxValue < p+c) maxValue = p+c
            return p+c
        },0)

        return maxValue
    }

   
```




##other solution

- 모든값을 더하여 sum 변수에 저장하고 min변수에 0과 합의 최소값을 저장한다.(min은 0 이상이될수가없다.)
- 결과값에 sum-min변수와 자신을 비교하여 최대값을 저장한다.(max는 0 이하가 될 수 없다.)
- 이해하는것도 한참걸림... 수학공부가 필요할 것 같다.


```javascript

    var maxSequence = function(arr){
    var min = 0, ans = 0, i, sum = 0;
        for (i = 0; i < arr.length; ++i) {
            sum += arr[i];
            min = Math.min(sum, min);
            ans = Math.max(ans, sum - min);
        }
        return ans;
    }

```


