## 1. 정규 표현식
> 정규 표현식 (Regular Expression)
>> 필요성, 파이썬에서의 기본 사용법, 코드 예제  
  
  
## 2. 정규 표현식이란?
정규표현식 (Regular expressions) 은 특정한 규칙을 가진 문자열의 집합을 표현하는 데 사용하는 형식 언어이다. 복잡한 문자열의 검색과 치환을 위해 사용한다.  

## 3. 정규 표현식 문법

|특수 문자	|설명 |
|:---:|:---|
|.|	한 개의 임의의 문자를 나타낸다. (줄바꿈 문자인 \n는 제외)|
|?	|앞의 문자가 존재할 수도 있고, 존재하지 않을 수도 있다. (문자가 0개 또는 1개)|
|*	|앞의 문자가 무한개로 존재할 수도 있고, 존재하지 않을 수도 있다. (문자가 0개 이상)|
|+	|앞의 문자가 최소 한 개 이상 존재한다. (문자가 1개 이상)|
|^	|뒤의 문자열로 문자열이 시작된다.|
|$	|앞의 문자열로 문자열이 끝난다.|
|{숫자}|	숫자만큼 반복한다. 
|{숫자1, 숫자2}|	숫자1 이상 숫자2 이하만큼 반복한다. ?, *, +를 이것으로 대체할 수 있다.|
|{숫자,}|	숫자 이상만큼 반복한다.|
|[ ]|	대괄호 안의 문자들 중 한 개의 문자와 매치한다. [amk]라고 한다면 a 또는 m 또는 k 중 하나라도 존재하면 매치를 의미한다. [a-z]와 같이 범위를 지정할 수도 있다. [a-zA-Z]는 알파벳 전체를 의미하는 범위이며, 문자열에 알파벳이 존재하면 매치를 의미한다.|
|[^문자]|	해당 문자를 제외한 문자를 매치한다.|
|l|	AlB와 같이 쓰이며 A 또는 B의 의미를 가진다.|

 --- 
##### [] 문자 클래스

-를 사용하면 두 문자 사이의 범위를 뜻한다.
```python
[abc] # abc 중 하나와 매치
'a' # a와 매치
'boy' # b와 매치
'dye' # a, b, c 중 어느 문자와도 매치되지 않음

[a-c] # [abc]와 같음
[0-5] # [012345]와 같음
[a-zA-Z] # 모든 알파벳
[0-9] # 숫자
```

---
[] 안에서 ^는 반대를 뜻한다.
```python
[^0-9] # 숫자를 제외한 문자만 매치
[^abc] # a, b, c를 제외한 모든 문자와 매치
```
---

##### . 모든 문자

.은 줄바꿈 문자인 \n 을 제외한 모든 문자와 매치된다.
```python
a.b # 'a + 모든 문자 + b'를 뜻함
aab # a와 b 사이의 a는 모든 문자에 포함되므로 매치
a0b # a와 b 사이의 0은 모든 문자에 포함되므로 매치
abc # a와 b 사이에 문자가 없기 때문에 매치되지 않음
```

---
[] 사이에서 .을 사용할 경우 문자 원래의 의미인 마침표가 된다.
```python
a[.]b
a.b # a와 b 사이에 마침표가 있으므로 매치
a0b # a와 b 사이에 마침표가 없으므로 매치 안됨
```
---

##### * 반복

* 앞에 오는 문자가 0개를 포함하여 몇 개가 오든 모두 매치된다.
```python
ll # 매치
lol # 매치
looool # 매치
looooooooooooooooooooool # 매치
lbl # 매치 안됨
loooooooooooobooooooool # 매치 안됨
```
---

##### + 최소 한 번 이상 반복

+ 앞에 있는 문자가 최소 한 번 이상 반복되어야 매치된다.
```python
lo+l
ll # 매치 안됨
lol # 매치
looooool # 매치
```
---
##### ? 없거나 하나 있거나
? 앞에 있는 문자가 없거나 하나 있을 때 매치된다.

```python
lo?l
ll # 매치
lol # 매치
lool # 매치 안됨
```

---

##### {m, n} 반복 횟수 지정

{m, n} 앞에 있는 문자가 m 번에서 n 번까지 반복될 때 매치된다.

```python
lo{3, 5}l
 ll # 매치 안됨
 lol # 매치 안됨
 loool # 매치
 loooool # 매치
 looooool # 매치 안됨
```
{m}의 형태로 사용하면 반드시 m 번 반복인 경우만 매치된다.

{0,} 는 *, {1,} 는 +, {0,1} 는 ? 와 각각 동일하다.

---
##### | 여러 개의 표현식 중 하나
여러 개의 정규표현식들을 | 로 구분하면 or 의 의미가 적용되어 정규표현식들 중 어느 하나와 매치된다.
```python
a|b|c # hello or hi or bye
a # 매치
b # 매치
c # 매치
a b # 매치
a b c # 매치
d # 매치 안됨
```
---
##### ^ 문자열의 제일 처음과 매치
문자열이 ^의 뒤에 있는 문자로 시작되면 매치된다. 여러 줄의 문자열일 경우 첫 줄만 적용된다. (단, re.MULTILINE 옵션이 적용되면 각 줄의 첫 문자를 검사하여 매치된다.)
```python
^a
a # 매치
aaa # 매치
baaa # 매치 안됨
1aaa # 매치 안됨
```
---
##### $ 문자열의 제일 마지막과 매치
문자열이 $의 앞에 있는 문자로 끝나면 매치된다. 여러 줄의 문자열일 경우 마지막 줄만 적용된다. (단, re.MULTILINE 옵션이 적용되면 각 줄의 마지막 문자를 검사하여 매치된다.)
```python
a$
a # 매치
aa # 매치
baa # 매치
aabb # 매치안됨
```
---
##### \A , \Z
\A 는 ^ 와 동일하지만 re.MULTILINE 옵션을 무시하고 항상 문자열 첫 줄의 시작 문자를 검사한다. \Z 는 $ 와 동일하지만 re.MULTILINE 옵션을 무시하고 항상 문자열 마지막 줄의 끝 문자를 검사한다.

---

## 4. 정규 표현식의 사용

#### 모듈 import
Python 에서는 re 모듈을 통해 정규표현식을 사용한다.
```python
import re
```
---

#### compile 정규표현식 컴파일
re.compile() 명령을 통해 정규표현식을 컴파일하여 변수에 저장한 후 사용할 수 있다.
정규표현식을 컴파일하여 변수에 할당한 후 타입을 확인해보면 _sre.SRE_Pattern 이라는 이름의 클래스 객체인 것을 볼 수 있다.
```python
변수이름 = re.compile('정규표현식')

p = re.compile('[abc]')
print(type(p))
```
---

#### 패턴 객체의 메소드
예시는 아래 코드를 사용한다.
```python
p = re.compile('[a-z]+')
```
---
##### match: 시작부터 일치하는 패턴 찾기
문자열의 처음 시작부터 검색하여 일치하지 않는 부분이 나올 때까지 찾는다.
```python
p.match('aaaaa')
<_sre.SRE_Match object; span=(0, 5), match='aaaaa'>

p.match('bbbbbbbbb')
<_sre.SRE_Match object; span=(0, 9), match='bbbbbbbbb'>

p.match('1aaaa')
None

p.match('aaa1aaa')
<_sre.SRE_Match object; span=(0, 3), match='aaa'>
```
검색 결과 : _sre.SRE_Match 객체 리턴

---
##### search: 전체 문자열에서 첫 번째 매치 찾기
문자열 전체에서 검색하여 처음으로 매치되는 문자열을 찾는다.
```python
p.search('aaaaa')
<_sre.SRE_Match object; span=(0, 5), match='aaaaa'>

p.search('11aaaa')
<_sre.SRE_Match object; span=(2, 6), match='aaaa'>

p.search('aaa11aaa')
<_sre.SRE_Match object; span=(0, 3), match='aaa'>

p.search('1aaa11aaa1')
<_sre.SRE_Match object; span=(1, 4), match='aaa'>
```
match와 동일한 형태로 결과를 출력해준다.

---
##### findall: 모든 매치를 찾아 리스트로 반환
문자열 내에서 일치하는 모든 패턴을 찾아 리스트로 반환한다.
```python
p.findall('aaa')
['aaa']

p.findall('11aaa')
['aaa']

p.findall('1a1a1a1a1a')
['a', 'a', 'a', 'a', 'a']

p.findall('1aa1aaa1a1aa1aaa')
['aa', 'aaa', 'a', 'aa', 'aaa']
```
---

##### finditer: 모든 매치를 찾아 반복가능 객체로 반환

```python
p.finditer('a1bb1ccc')
<callable_iterator object at 0x7f850c4285f8>
//callable_iterator라는 객체가 반환

//for문을 사용하여 하나씩 출력
f_iter = p.finditer('a1bb1ccc')
for i in f_iter:
    print(i)
```

출력 결과  
<_sre.SRE_Match object; span=(0, 1), match='a'>  
<_sre.SRE_Match object; span=(2, 4), match='bb'>  
<_sre.SRE_Match object; span=(5, 8), match='ccc'>  

---

