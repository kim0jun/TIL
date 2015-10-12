last chair
================

##문제

n개의 1렬로된 의자가있다. 의자는 1~n까지 번호가 매겨져있다. 1번은 출구에서 가장가깝다.

어떤 이유에서 사람들은 다음과 같은 규칙으로 의자에 앉았다.
1. 다른사람과 최대한멀리 떨어져서
2. 최대한 출구와 가까이

모드의자들은 첫번째 사람이 앉기전에 세팅된다.


Chairs   | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  | 10
---------|---|---|---|---|---|---|---|---|----|---
Patients | 1 | 7 | 5 | 8 | 3 | 9 | 4 | 6 | 10 | 2


##my solution

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

- 현재 통과하지못함 동작은 제대로 하나 시간이 너무 오래걸리기때문  -> 반복문을 너무 많이 써서 그런듯 개선해야함