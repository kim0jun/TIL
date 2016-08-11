Reverse polish notation calculator


=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

당신의 할일은 역 폴란드 표기법의 값을 구하는 계산기르 만드는것 입니다..

예를들어 `5 1 2 + 4 * + 3` - (보통 계산식의  `5 + ((1 + 2) * 4) - 3` 와 같다.) 의 계산식은 14의 값을 구해야 합니다.

당신이 알아두어야할것은 그것들은 항상 숫자,연산자 사이에 공백이 들어갑니다.
예를들어 `1 3 +` 은 유효한 식 이지만, `1 3+`은 그렇지 않습니다.

빈 계산식의 경우에는  `0` 의 값이 구해질 것입니다.

유효한 연산자 는 `+`,`-`,`*`,`/` 입니다.

당신은 예외적인 상황이 없다는걸 알고 있습니다.(부동수점이나 0으로 나누기같은)












###작업내용
 

```

calc(`5 1 2 + 4 * + 3`)  => 14

```



##my solution

- 각 숫자,연산자를 담는 배열을 만들자
- 재귀 함수를 이용하여 해결하자

```javascript

function calc(expr) {
  //공백기준으로 배열로 나눠잡기
  var __exprArr = expr.split(" ");
  //만약 빈 계산식이라면 0을 반환한다.
  if(expr.length === 0) return 0
  //그렇지않다면 계산식을 적용한다
  return reversePolishNation(__exprArr,[])
}

//역 폴란드 계산식 함수( 파라미터로는 두개의 배열을 가진다. 원 식 배열, 숫자 스택 배열 )
function reversePolishNation(originArr,numStack) {
    //만약 계산식을 만난다면  넘버스택 마지막과,그전숫자를 구하여 연산식을 적용하여 다시 넘버스택에 쌓는다. 만약 계산식이 아니라면 넘버스택에 쌓는다.
    switch (originArr[0]) {
        case "+" : var __b = numStack.pop()*1;
                   var __a = numStack.pop()*1;
                   numStack.push(__a+__b); break;
        case "*" : var __b = numStack.pop()*1;
                   var __a = numStack.pop()*1;
                   numStack.push(__a*__b); break;
        case "-" : var __b = numStack.pop()*1;
                   var __a = numStack.pop()*1;
                   numStack.push(__a-__b); break;
        case "/" : var __b = numStack.pop()*1;
                   var __a = numStack.pop()*1;
                   numStack.push(__a/__b); break;
        default  : numStack.push(originArr[0]);
            break;
    }
    
    // 만약 배열을 모두사용했다면 값을 반환
    if(originArr.length <= 1) return numStack[numStack.length-1]*1 || 0
    // 아니라면 재귀함수 호출 
    else                      return reversePolishNation(originArr.slice(1),numStack)
}

   
```




##other solution

- 함수식이 하나로 훨씬간편하다 (내가 어렵게 생각한듯)
- 전체적으로 문제를 이해한 방식은 나와같다. 대신 이사람은 반복문을 사용함
- 반복문이 더 효율적인듯  내함수에는 불필요한 부분이 더 많다. (매번 배열을 할당)
- `/` 일때  `b/a` =>  `1/(a/b)` 인건 알아두자 
- parseFloat함수는 문자열 배열에서 첫번째로 찾은 숫자를 반환한다(number형으로)

```javascript

   function calc(expr) {  
      var result = [];
      var atoms = expr.split(/\s+/);
      var operators = ['+', '-', '*', '/'];
      for (var i=0; i<atoms.length; i++) {
        switch(atoms[i]) {
          case '+': result.push(result.pop() + result.pop()); break;
          case '-': result.push(-result.pop() + result.pop()); break;
          case '*': result.push(result.pop() * result.pop()); break;
          case '/': result.push(1 /(result.pop() / result.pop())); break;
          default: result.push(parseFloat(atoms[i]));
        }
      }
      return result.pop() || 0;
    }   

```

- 리듀스와 , 오브젝트를 영리하게잘사용하였
- 리듀스문 반복돌면서 연산자를 만나면 식을 계산하고 만약 현재 값이 연산자면 연산 아니라면 스택에쌓
- +(문자열)은 number타입으로 치환된다.

```javascript
    var operands = {
      '+': function (b, a) { return a + b;},
      '-': function (b, a) { return a - b;},
      '*': function (b, a) { return a * b;},
      '/': function (b, a) { return a / b;}
    };

    function calc(expr) {
      expr = expr || '0';
      return +expr.split(/\s/g).reduce(function (stack, current) {
          stack.push(operands[current] ? operands[current](+stack.pop(), +stack.pop()) : current);
        return stack;
      }, []).pop();
    }

```
