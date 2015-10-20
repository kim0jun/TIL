Unique In Order
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

파라메터로 배열이나,문자열을 넣으면 연속해서 있는 문자,숫자를 제거해서 배열로 리턴해주는 함수를만들어라


###작업내용
 

```
uniqueInOrder('AAAABBBCCDAABBB') == ['A', 'B', 'C', 'D', 'A', 'B']
uniqueInOrder('ABBCcAD')         == ['A', 'B', 'C', 'c', 'A', 'D']
uniqueInOrder([1,2,2,3,3])       == [1,2,3]

```



##my solution


- 만약 문자열이면 정규식을 이용해서 배열로만들자
- 배열내 반복을이용해서 이전값과 다르면 새로운 배열에 쌓자 그다음 반환

```javascript

    var uniqueInOrder=function(iterable){
        if(iterable.length == 0 ) return []
        var uniqueArr =  []
        iterable = (typeof(iterable) == "object")? iterable:iterable.match(/\d|\w/g)
        iterable.reduce(function (prev,current,index,arr) {
            if(prev != current) uniqueArr.push((/\d/.test(current))?   current*1: current) 
            return current
        },[])
        return uniqueArr
    }
   
```




##other solution

- 엄청 간단하게 코드를 짯다.
- 전역변수로 last라는 변수를만들고 배열에 집어넣을때값을 last에 저장해서 이전값과 비교한다.
- 문자열도 배열처럼 [n]형식으로 접근가능하다는걸 처음 알았다.


```javascript

    function uniqueInOrder(it) {
        var result = []
        var last

        for (var i = 0; i < it.length; i++) {
            if (it[i] !== last) {
                result.push(last = it[i])
            }
        }

    return result
}    

