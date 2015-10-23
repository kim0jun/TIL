Counting Duplicates
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

오늘도 시간관계상 번역은 생략, 문자열을 읽어서 두번이상 나온 알파벳의 갯수를 반환하여라.(대소문자 구분없이)


###작업내용
 

```
"abcde" -> 0 # no characters repeats more than once
"aabbcde" -> 2 # 'a' and 'b'
"aabbcdeB" -> 2 # 'a' and 'b'
"indivisibility" -> 1 # 'i'
"Indivisibilities" -> 2 # 'i' and 's'

```



##my solution

- 대문자나, 소문자로 통일한후
- for문을 돌려서 자신이후의 알파벳중 반복되는 알팝벳이있고, 이 알파벳이 기존에 반복카운트를 올린 문자열이 아니라면 카운트를 올린다.

```javascript

    function duplicateCount(text){
        //텍스트를 소문자로(통일)
        text = text.toLowerCase();
        var stackStr = ""
        var duplicateCount = 0
        for(var i=0;i<text.length;i++){
            if(text.substr(i+1).search(text[i]) != -1  && stackStr.search(text[i]) == -1 ){
                stackStr += text[i]
                duplicateCount++
            }
        }
        return duplicateCount
    }

   
```




##other solution

- 엄청 영리하게 짯다.. 나는 요즘 시간없다는 이유로 너무 딱딱한 방식으로만 접근하는것같다.. 반성해야함..
- 문자열을 모두 소문자로바꾼이후에 배열에담고 sort 함수를 이용해서 차례대로 정리한후에 join을이용해서 문자열로 바꾼후
- /([^])\1+/g 라는 정규식을 이용해서 2번이상 연속되는 알파벳을 찾아서 배열을만들고 이 배열의 길이를 반환
- 이때 정규식을 하나도 만족하지않으면 빈배열이아니라 null이 들어옴으로 || [] 을 추가한다.


```javascript

    function duplicateCount(text){
        return (text.toLowerCase().split('').sort().join('').match(/([^])\1+/g) || []).length;
    }
}    

