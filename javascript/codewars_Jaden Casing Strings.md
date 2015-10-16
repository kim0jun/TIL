Jaden Casing Strings
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

윌스미스의 아들 제이든 스미스는  가라테키드, 에프터어스 등을 찍은 영화 스타다.제이든은 또한 트위터에 그의 생각(철학)을 올리는것으로도 알려져있다.
트위터에 글을 쓸 때, 그의 모든 단어를  거의  대문자로 시작한다.

**당신의 과제는 문자열들을 제이든 스미스가 쓴것처럼 변화 시키는것이다.** 이 문자열들은 사실 제이든 스미스의 글들을 인용하였다.
그러나 원글처럼 대문자로 시작하지는 않는다.



###작업내용


```

Not Jaden-Cased: "How can mirrors be real if our eyes aren't real"
Jaden-Cased:     "How Can Mirrors Be Real If Our Eyes Aren't Real"
    

```



##my solution

- 매단어를 찾기위하여 띄어쓰기(" ")를 이용하여 문자열을 자르고 해당문자열을 담는 배열을 만들자.
- map을 이용하여 배열내에서 반복문을 만들자.
- 만약 index가 0 이라면 앞에 띄어쓰기를 붙이지않고(맨 단어임으로) 아니라면 띄어쓰기를하자(원래대로)
- 단어의 첫단어를 대문자로 변화시키고, 나머지는 소문자로 변화하여 반환할 문자열에 붙이자.
- it's too easy


```javascript

    String.prototype.toJadenCase = function () {
        var jadenStr = ""
        this.split(" ").map(function(str,index){
            if(index != 0) jadenStr += " "
            jadenStr += str.charAt(0).toUpperCase() + str.substring(1).toLowerCase()
        })
        return jadenStr;
    };

   
```




##other solution

- 단어들을 잘라내는 방법은 나와 같으나 join() 이라는 함수를 사용해서 보다 간단하게 코드를 짰다.
- join()은 Array의 함수로  array 모든 문자열을 합쳐서 문자열로 반환한다. 사이에 파라메터를 삽입한다.
- 그래서 불필요한 조건문이없기때문에 나도 다음부터는 이방법을 사용할거같다.

```javascript

    String.prototype.toJadenCase = function () { 
        return this.split(" ").map(function(word){
            return word.charAt(0).toUpperCase() + word.slice(1);
        }).join(" ");
    }

```

- 정규표현식을 이용하여 단어의 첫번째 스펠링을 찾아서 대문자로 치환하였다.
- (^|\s)는 ^ 문자열의시작  또는 \s 빈공간을 찾습니다.
- 바로뒤에붙은[a-z]를 사용하여 단어의시작+바로뒤에붙은 소문자를 찾는패턴을 완성합니다.
- 정규식중 g 는 문자열 내의 모든 패턴을 찾습니다(global)
- 정규식도 상당히 유용함으로 간단한 사용법을 익혀야 할 것 같다. 
 
```javascript

    String.prototype.toJadenCase = function () {
        return this.replace(/(^|\s)[a-z]/g, function(x){ return x.toUpperCase(); });
    };

```
