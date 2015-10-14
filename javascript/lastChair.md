last chair
=============================================
[codewars](www.codewars.com) 에서 오늘 내가 푼 문제

##문제

n개의 1렬로된 의자가있다. 의자는 1~n까지 번호가 매겨져있다. 1번은 출구에서 가장가깝다.

어떤 이유에서 사람들은 다음과 같은 규칙으로 의자에 앉았다.
1. 다른사람과 최대한멀리 떨어져서
2. 최대한 출구와 가까이

모든의자들은 첫번째 사람이 앉기전에 세팅된다.

ex)

Chairs   | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  | 10
---------|---|---|---|---|---|---|---|---|----|----
Patients | 1 | 7 | 5 | 8 | 3 | 9 | 4 | 6 | 10 | 2

이때 n명 중에서 마지막에 앉은사람의 의자위치를 구하여라


##my solution

입장 --> 위치선정 --> 다음사람입장 --> 위치선정  ...반복 -> 마지막사람입장 -> 위치선정 -> 반환

```javascript

function lastChair($num){
//의자를 세팅한다.
    this.chairs = []
    for(var i=0;i<$num;i++){
        this.chairs.push(0)
    }
//한명씩 차례대로 착석시킨다.
    for(var patientNum = 0 ; patientNum <$num;patientNum++){
        // 다른사람과 얼마나 먼지알수있는 배열을 만든다.(첫번째규칙)
        var distance = []
        // n개의 의자에대해서 한번씩실행한다.
        for(var x = 0 ; x <$num;x++){
            // 만약 현재의자에 사람이앉아있다면 간격은 0으로설정한다.
            if (chairs[x] != 0)  distance.push(0)
            else { 
                distance.push(chairs.reduce(function(pre,current,index) {
                    //해당자리가 현재검색하는 자리와같거나,해당자리에 아무도 앉지않았다면 다음자리를 검색한다.
                    if(index == x || chairs[index]== 0) {
                        return pre
                    }
                    var newDis = (x > index)? x-index:index-x
                    return (pre <= newDis)? pre:newDis
                },$num))
            }

        }
        //가장 다른자리와 거리가멀고,입구에서 가까운자리를 찾느다.
        crurrentPatient = distance.reduce(function (prev,current,index) {
            return (distance[prev]>=distance[index])? prev:index
        },0)
        //찾은자리에 착석시킨다.
        this.chairs[crurrentPatient] = patientNum+1;	
    }
    //배열은 0부터시작하지만 실제자리는 1번부터있으므로 +1해서 리턴한다.
    return crurrentPatient+1
}

```


- 현재 통과하지못함 동작은 제대로 하나 시간이 너무 오래걸리기때문(타임아웃 ㅠ)  -> 반복문을 너무 많이 써서 그런듯 
- 코드를 다시짜려고 했으나.. 결국 포기하고 다른사람들코드를 봄


##other solution

- 다들 내생각보다 쉽게풀었다.
- 3명 미만일 때 위치는 n번째이고 3명 이상일 때 는 n-1번째가 제자리다.

```javascript

    function lastChair(N){
        return N < 3 ? N : N - 1;
    }

```

- 빈공백사이를 구함  
- 이게 내가짠코드보다 훨씬 더 좋은코드다. -> 무의미한 연산의 최소화

```javascript

function lastChair(N){

    return N-1; // what was the point of this??  -> 이 사람도 결국엔 이렇게 푼듯 ㅋㅋㅋ

    var seat;  
    var ranges = [];

    ranges[0] = createRange(0, N-1);   // 첫번째 공백을구함(첫번째는 0번째,마지막번호는 n-1번자리에 자동착석)

    // find candidate range 
    for(var i = 2; i < N; i++) {
        //for문내에서 사용할 변수 세팅  
        var largestSize = 0;  //가장먼곳
        var candidateRangeIdx = 0;
        var smallestStart = N-1;

        // find the largest range closest to index 0 ->  현재 생성된 공간만큼 반복
        for(var j = 0; j < ranges.length; j++) {
            // look for the biggest range  -> 이전 공간보다 큰공간을 찾으면 그공간의 값들을 저장
            if(ranges[j].size() > largestSize) {
            
                largestSize = ranges[j].size();
                smallestStart = ranges[j].start();
                candidateRangeIdx = j;
            }

            // look for a range the same size but closer to index 0  
            // -> 같은 크기의 공간 이나 0에서 더가까울때   최대공간값을 제외한값들을 업데이트
            if(ranges[j].size() == largestSize && ranges[j].start() < smallestStart) {
                smallestStart = ranges[j].start();
                candidateRangeIdx = j;
            }

            //->위 두개의 if문을하나로 줄여보았다.(똑같이 작동한다)
            //=============================================================================
            /* 
            if(ranges[j].size() > largestSize || 
               (ranges[j].size() == largestSize && ranges[j].start() < smallestStart)){
                largestSize = ranges[j].size();
                smallestStart = ranges[j].start();
                candidateRangeIdx = j;
            }
            */
            //=============================================================================
        }

        if(ranges[candidateRangeIdx].size() % 2 == 0) { // even -> 짝수와 홀수분기
            //seat는 함수내 전역변수
            //공간의 절반 + 공간의시작점에 앉힘
            seat = Math.floor(ranges[candidateRangeIdx].size() / 2) + ranges[candidateRangeIdx].start();
        } else { // odd -> 홀수면
            //홀수의 경우에는 절반 + 공간시작점 +1(공간의 크기를 나눌때 내림하였음으로 1증가 시켜줘야함)
            seat = Math.floor(ranges[candidateRangeIdx].size() / 2) + ranges[candidateRangeIdx].start() + 1;
        }

        // split range into two ranges -> 공간을 반으로쪼갬
        // 공간배열 맨뒤에 새롭게 앉은 사람의 값을 추가
        ranges[ranges.length] = createRange(seat, ranges[candidateRangeIdx].end());
        // 기존공간배열 값 업데이트
        ranges[candidateRangeIdx] = createRange(ranges[candidateRangeIdx].start(), seat);
    }

    return seat + 1;
}


var createRange = function(s, e) {

    var _start = s; //시작
    var _end = e; //끝
    var _size = e - s - 1; //길이

    var _getSize = function() {
        return _size;
    };

    var _getStart = function() {
        return _start;
    };

    var _getEnd = function() {
        return _end;
    };

    var _toString = function() {
        return "start " + _getStart() + " end " + _getEnd() + " size " + _getSize();
    };

    return {
        start: _getStart,
        size: _getSize,
        end: _getEnd,
        toString: _toString
    };
}

```

