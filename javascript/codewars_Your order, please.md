Your order, please
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

당신이 해야할 것은 받은 문자열들을 소팅하는것이다. 각가의 단어들은 문자열안에 하나의 숫자들을 포함하고있다. 
그숫자들은 결과에서의 단어의 위치이다.

노트 : 숫자는 1-9까지이다. 그러므로 1은 무조건 첫번째 단어일것이다 (0이아니라)

만약 문자열을 입력하지않는다면, 빈문자열을 반환할것이다. 입력되는 단어 문자열속 숫자들은 연속적인 숫자들로만 나온다.







###작업내용
 

```

order("is2 Thi1s T4est 3a")  =>  "Thi1s is2 3a T4est"

```



##my solution

- 각 단어들을 담는 배열을만든후, 각단어들의 숫자를 추출하는 함수를 이용하여 소팅하자
- 소팅은 퀵소트를 이용하자 (기준값을 기준으로 앞뒤배열을 만든후 붙이는 밥법으로 소팅하는 방식)

```javascript

function order(words){
    var wordArr = words.split(" ")
    return wordsQuickSort(wordArr,wordArr.length).join(" ");
}

//quick_sort   a는 배열  n은 length
function wordsQuickSort(a, n) {
    // 배열 길이가 1이하면 원래 배열을 반환
    if(n<=1) return a
    // 배열의 길이가 2면 두개의 값만 비교하여 swap함
    if(n==2){
        if(numberOfWord(a[0]) > numberOfWord(a[1])){
            var x = a[0];
            a[0] = a[1];
            a[1] = x;
        }
        return a
    }

    //배열의 길이가 3이면 퀵소트(피벗을 기준으로 앞뒤로 나눠야하기 때문에 3이상이여야 한다)
    // 피벗 = 기준값
    var pivot = a[0];

    // 앞 뒤 배열을만들고
    var left = [];
    var right = []; 

    // 배열에 관한 카운트를 만듬
    var left_pos = 0;
    var right_pos = 0;

    // 배열에 대한 반복
    for(i = 1; i< n; ++i){
        // 피벗보다 크면 left배열에 아니라면 right 배열에 쌓는다.
            if(numberOfWord(a[i]) <= numberOfWord(pivot))	 			left[left_pos++] = a[i];
        else 			    			 
            right[right_pos++] = a[i];
    }

    //나눠진 앞,뒤 배열에 다시 퀵소트 재귀함수
    left = wordsQuickSort(left, left_pos);
    right = wordsQuickSort(right, right_pos);

    // 좌측,피벗,우측 순으로 배열을 다시만든후 반환
    var pos = 0
    for(i = 0; i<left_pos;++i) a[pos++] = left[i];
    a[pos++] = pivot
    for(i = 0; i<right_pos;++i) a[pos++] = right[i];

    return a
}

// 단어에서 숫자를 찾아서 반환하는 함수 
var numberOfWord = ($word) => {return  /\d/.exec($word)[0]}


   
```




##other solution

- 엄청 간단하게 코드를 짯다.
- array와 string의 기본함수를 잘이용한것같다.
- 가독성도 높아서 효율적이다.
- sort함수는   Array.sort(a-b) 일 경우 오름차순으로 소팅, Array.sort(b-a) 일 경우 내림차순으로 소팅된다. 기본값은 a-b
- 나도 소트함수를 썻으면 더쉬웠을것같지만 퀵소트를 이해 할 수 있었던 좋은 기회였다.


```javascript

    function order(words){
        return words.split(' ').sort(function(a, b){
            return a.match(/\d/) - b.match(/\d/);
        }).join(' ');
    }    

```

- 바로 위코드와 같은 방법으로 소팅 그리고 단어에서 숫자를 찾는방법은 나와같다. 
- \d+ 를이용하여 10이상 숫자도 소팅할수있게하였다.(하지만 문제에서 9까지였음으로 불필요)

```javascript
    const order = words => words.split(' ').sort((a, b) => +/(\d+)/.exec(a)[0] - +/(\d+)/.exec(b)[0]).join(' ');

```
