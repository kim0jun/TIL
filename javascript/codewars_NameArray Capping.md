last chair
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

이름 배열을 입력받아서 첫번째 스펠링만 대문자로 반환한 배열을 반환하는 methode를 만들어라.


```javascript
    capMe(['jo', 'nelson', 'jurie'])     // returns ['Jo', 'Nelson', 'Jurie']
    capMe(['KARLY', 'DANIEL', 'KELSEY']) // returns ['Karly', 'Daniel', 'Kelsey']

```





##my solution

-  이름배열 반복문 -> 이름을 쪼개서 반복문 -> 조건에 부합하는지에 따라 차례대로 반환

```javascript
function capMe(names) {
    //배열에대한 반복
    return names.reduce(function(nameArray,current,index){
        //이름에대한반복
        var name = current.split("").reduce(function (name,letter,index) {
            var asciiCode = letter.charCodeAt();
            // 첫번째 index인가?  만약그렇다면 소문자인가?
            if(index == 0) name += (asciiCode > 96)?  String.fromCharCode(asciiCode - 32):String.fromCharCode(asciiCode)
            // 첫번째 인덱스가 아니라면 혹시 대문자인가??
            else           name += (asciiCode > 96)?  String.fromCharCode(asciiCode):String.fromCharCode(asciiCode+32)
            //이름을 반환
            return name
        },"")
        nameArray.push(name)
        return nameArray
    },[])
    }
   
```



##other solution

- 엄청심플하다. map이라는 함수는 한번도 안써봤는데 한번 써봐야겠다. map은 배열의 각요소에 접근해서 그 결과로 새로운 배열을 만드는 함수이다.
- string에 좋은 methode가 많은데 나는 그걸 사용하지않고있엇다. 
- chartAt(0)으로 0번째인 첫번째 숫자를 toUpperCase() 로 대문자로 만들수있다.
- substring(1)은 1번째 이후의 문자열을 새로반환한다. 이 문자들을  toUpperCase()로 소문자로 반환.

```javascript
function capMe(names) {
        return names.map(function (n) { return n.charAt(0).toUpperCase() + n.substring(1).toLowerCase(); });
    }
```



