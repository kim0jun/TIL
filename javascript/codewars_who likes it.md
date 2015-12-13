Counting Duplicates
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

당신은 십중팔구 페이스북이나 다른 페이지의 '좋아요'시스템을 알것이다.  사람들은 블로그 포스트나 사진 등등의것에 좋아요를 누를수있다.
우리는 다음과같이 보이는 문장을 만들고싶다.   ```likes :: [String] ->String```
해당 아이템을 좋아하는 사람들의 이름이 담겨있는 배열을 가져와야한다. 그리고 예제처럼 보이는 문장을 출력해야한다.


###작업내용
 

```
likes [] // must be "no one likes this"
likes ["Peter"] // must be "Peter likes this"
likes ["Jacob", "Alex"] // must be "Jacob and Alex like this"
likes ["Max", "John", "Mark"] // must be "Max, John and Mark like this"
likes ["Alex", "Jacob", "Mark", "Max"] // must be "Alex, Jacob and 2 others like this"

```



##my solution

- 스위치문을 이용해서 배열길의가  0,1,2,3 그리고 4이상일경우를 분기해서 반환하자.
- 0,1 일때는 3인칭단수임으로 'likes' 그리고 2이상일 때는 복수임으로 'like'를 써야한다. 여기에는 if문을 이용해서 분기하자.

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

-  나와 비슷하게 짰다. 하지만 만약 뒤에 문장이 변한시 일일히 바꿔줘야해서 귀찮기때문에 내방식이 좀더 좋은것같다.
-  하지만 내방식과 이사람방식을합쳐서  미리 뒤에 출력할 단어를 가진 배열을 만들어두고 그 변수를 이용해서 문장을 만들면 더좋았을거같다. (수정도 간단하고(이 함수의 문제점) , 불필요한 연산도 제거할수있다(나의방식의 문제점))


```
    function likes(names) {
        names = names || [];
        switch(names.length){
            case 0: return 'no one likes this'; break;
            case 1: return names[0] + ' likes this'; break;
            case 2: return names[0] + ' and ' + names[1] + ' like this'; break;
            case 3: return names[0] + ', ' + names[1] + ' and ' + names[2] + ' like this'; break;
            default: return names[0] + ', ' + names[1] + ' and ' + (names.length - 2) + ' others like this';
        }
    }

```


- 이렇게 짜는건 생각도 못했는데 엄청 영리한것같다. 앵귤러js가 이런식으로 동작하는것일까 ?

```
    function likes (names) {
        //문장배열은만든다.
        var templates = [
            'no one likes this',
            '{name} likes this',
            '{name} and {name} like this',
            '{name}, {name} and {name} like this',
            '{name}, {name} and {n} others like this'
        ];
        //인덱스 변수인데 최대4를반환하도록 작성하였다. 좋은 응용법인것같다.( Math.min은 어규먼트중 더작은 값을 반환하는 함수)
        var idx = Math.min(names.length, 4);
        
        //처음만든 문장배열을 반환하되 {name}과 {n}에 names배열의 값을 적용한다. {names}에 텍스트를 덮어쓸때마다 shift()를 이용해서 배열을하나씩제거
        return templates[idx].replace(/{name}|{n}/g, function (val) {
            return val === '{name}' ? names.shift() : names.length;
        });
    }
```



