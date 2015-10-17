Jaden Casing Strings
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

문자열을 입력받는 함수를 만들어라, 그리고 만약 전화번호의 폼이라면 true를 반환해라
당현이 그것들은 0-9의 숫자들로 이루어져있을것이다. 유효한 전화번호로 만들어졌다면.

다음 포멧에 대해서만 걱정해라?(Only worry about the following format):
(123) 456-7890 ( 절대로 괄호를 닫은다음 나오는 공백을 잊지마라. )




###작업내용


```

validPhoneNumber("(123) 456-7890")  =>  returns true
validPhoneNumber("(1111)555 2345")  => returns false
validPhoneNumber("(098) 123 4567")  => returns false
    

```



##my solution

- 정규표현식을 이용하여 해결하자
- 앞에 정규표현식을 만드는것은 어렵지 않았는데 끝나는 정규표현식을 몰라서 해맸다.
- 정규표현식에서 x로 끝날때 x$로 표현한다.
- 어제 정규표현식을 사용해서 코드를 한번 짜보고 싶다고 하였는데 이틀연속 나와서 기분이 좋다.

```javascript

    function validPhoneNumber(phoneNumber){
        return (phoneNumber.search(/^\([0-9]{3}\)\s[0-9]{3}\-[0-9]{4}$/) == 0)?  true:false;
    }

   
```




##other solution

- 나는 String함수를 사용하였는데 다른 사람들은 정규표현식 함수를 사용하였다.
- 이쪽이 훨씬더 코드가 간단하고 효율적인것 같다.
- 특히 test함수는 문제에서 원하는 결과값에 아주 적합한 함수이다.
- test는 파라메터안의 문자열이 정규표현식과 일치한다면 true를 아니라면 false를 출력한다.

```javascript

    function validPhoneNumber(phoneNumber){
        return /^\(\d{3}\) \d{3}\-\d{4}$/.test(phoneNumber);
    }

```

- validPhoneNumber를 선언할때 bind를 사용하여 코드를 아주 간단하게 작성하였다.
- bind는 새로운 함수를 만들어내는 함수 인데 파라미터로 값으로 모듈을 사용한다.

```javascript

   var validPhoneNumber = RegExp.prototype.test.bind(/^\(\d{3}\) \d{3}-\d{4}$/);
   // validPhoneNumber = /^\(\d{3}\) \d{3}-\d{4}$/.test() 

```
