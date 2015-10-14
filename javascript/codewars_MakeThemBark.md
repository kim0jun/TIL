last chair
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

당신은 개 사육사에게 그의 개들을 기록하는 프로그램을 개발해주기로 하였다.

당신은이미 `Dog` constructor 만들어 놨다. 그래서 누구나 모든강아지들을 수동으로 기록할수도록

일은 다끝난것처럼 보였다. 그리고 당신이 돈을받기로 한때가 되었다.

잠깐! 그 개사육사가 말하길 모든 강아지 개체들이 `bark()`라는 동작을 하기전까지 돈을줄수없다고 하였다. 

심지어 이미 만들어진 개체들도. 사육사 왈 "모든 개가 짖게 해주세요", 그리고 그는 다시 기록하는걸 거부하였다. 얼마나 게으른지..


그는 엄청많은 개들을 가지고있었는데. 그것들중 누구도 `bark()`를  할수없었다.

당신을 이문제를 해결할수있습니가? 또는 이 클라이언트에게 제치있게 대응할수있을까요?



###작업내용

- `bark()`methode는 `Woof!`라는 문자열을 반환해야한다.
- 당신이 미리 만든 contructor는 이렇게 생겼다.

```javascript

function Dog(name, breed, sex, age){
    this.name  = name;
    this.breed = breed;
    this.sex   = sex;
    this.age   = age;
}
    

```




##my solution

-Dog 클래스에 prototype으로 `bark()`함수를 추가하자

```javascript

    Dog.prototype.bark = function(){
        return 'Woof!'
    }
   
```

- it's a easily  :)


##other solution

-이런식으로 함수를 사용해보는건 처음인데 간결하게 쓰기에 좋은 것 같다.  다음에는 간단한 함수는 이런식으로도 짜봐야겠다. 

```
Dog.prototype.bark = () => 'Woof!';
```

```
Dog.prototype.bark = x => 'Woof!';
```

```
Dog.prototype.bark = x => { return "Woof!" };
```