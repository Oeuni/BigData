# BigData


> 정규 표현식 (Regular Expression)
>> 필요성, 파이썬에서의 기본 사용법, 코드 예제

|특수 문자	|설명 |
|:---:|:---|
|.|	한 개의 임의의 문자를 나타냅니다. (줄바꿈 문자인 \n는 제외)|
|?	|앞의 문자가 존재할 수도 있고, 존재하지 않을 수도 있습니다. (문자가 0개 또는 1개)|
|*	|앞의 문자가 무한개로 존재할 수도 있고, 존재하지 않을 수도 있습니다. (문자가 0개 이상)|
|+	|앞의 문자가 최소 한 개 이상 존재합니다. (문자가 1개 이상)|
|^	|뒤의 문자열로 문자열이 시작됩니다.|
|$	|앞의 문자열로 문자열이 끝납니다.|
|{숫자}|	숫자만큼 반복합니다. 
|{숫자1, 숫자2}|	숫자1 이상 숫자2 이하만큼 반복합니다. ?, *, +를 이것으로 대체할 수 있습니다.|
|{숫자,}|	숫자 이상만큼 반복합니다.|
|[ ]|	대괄호 안의 문자들 중 한 개의 문자와 매치합니다. [amk]라고 한다면 a 또는 m 또는 k 중 하나라도 존재하면 매치를 의미합니다. [a-z]와 같이 범위를 지정할 수도 있습니다. [a-zA-Z]는 알파벳 전체를 의미하는 범위이며, 문자열에 알파벳이 존재하면 매치를 의미합니다.|
|[^문자]|	해당 문자를 제외한 문자를 매치합니다.|
|l|	AlB와 같이 쓰이며 A 또는 B의 의미를 가집니다.|

> 가비지 컬렉션 (Garbage Collection)
>> 필요성, 메커니즘, 코드
>>> 어떻게 하면 GC로도 메모리 leak이 발생될까?
