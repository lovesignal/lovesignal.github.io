---
key: 20190303
title: "[python] Pandas를 이용한 데이터 전처리 1"
excerpt: "pandas를 이용하여 특정 단어가 포함 되었는지 확인하는 방법"
categories: programming
comments: true
tag : [programming, python]
---



## 특정 단어가 포함 되었는지 확인하기

### 1. `contains`를 이용한 매칭

```python
import pandas as pd
word = pd.Series(['과일', '사과2개', '사과2개, 배1개', '배1개, 오렌지3개', '배한개, 딸기두개'])
word.str.contains('사과', regex=False)
---------------------------
0    False
1     True
2     True
3    False
4    False
dtype: bool
```



#### 두가지 단어 비교

```python
import pandas as pd
word = pd.Series(['과일', '사과2개', '사과2개, 배1개', '배1개, 오렌지3개', '배한개, 딸기두개'])
word.str.contains('사과|배', regex = True)
----------------------------
0    False
1     True
2     True
3     True
4     True
dtype: bool
```

`regex = True` 로 설정해주어야 한다. `False` 로 설정할 경우 정규표현식이 작동하지 않아서 False를 반환한다.

```python
# regex = False
import pandas as pd
word = pd.Series(['과일', '사과|배', '사과2개', '사과2개, 배1개', '배1개, 오렌지3개', '배한개, 딸기두개'])
word.str.contains('사과|배', regex=False)
----------------------------
0    False
1     True
2    False
3    False
4    False
5    False
dtype: bool
```



#### 숫자가 들어간 것 찾기

```python
import pandas as pd
word = pd.Series(['과일', '사과2개', '사과2개, 배1개', '배1개, 오렌지3개', '배한개, 딸기두개'])
word.str.contains('\d', regex=True)
----------------------------
0    False
1     True
2     True
3     True
4    False
dtype: bool
```





### 2. `re.search` or  `re.match` 이용

#### `re.search` 이용

```python
import re

compile_val = re.compile(r'라이언|무지|콘')
text = ['라이언과 무지는 친구이다.',
       '라이언과 콘도 친구이다.',
       '프로도와 네오는 연인이다.',
       '콘은 크로코다일과 콩알이 조합한 이름이다.',
       '무지는 토끼옷 입은 단무지이다.',
       '튜브는 소심한 오리이다.',
       '어피치는 유전자 변형으로 자웅동주가 된 것을 알고 복숭아 나무에서 탈출하였다.']

for i in text:
    if compile_val.search(i):
        print(i)
    else:
        print('FALSE')
---------------------------------------
라이언과 무지는 친구이다.
라이언과 콘도 친구이다.
FALSE
콘은 크로코다일과 콩알이 조합한 이름이다.
무지는 토끼옷 입은 단무지이다.
FALSE
FALSE
```



* if문에 직접 정규표현식을 넣으면 **매번 새로 compile 되므로** 변수에 할당해준 후 for문을 순환하는 것이 속도가 빠르다.

  0.0002초 밖에 안난다고 생각할 수 있지만, 정규식이 복잡해지고, 데이터가 수십만 건으로 늘어나서 for문 순환하게 되면 실행시간의 차이가 크다.

```python
# 정규표현식 컴파일을 변수에 할당한 후 for문 실행

import time
start = time.time()
#------------------
import re

compile_val = re.compile(r'라이언|무지|콘')
text = ['라이언과 무지는 친구이다.',
       '라이언과 콘도 친구이다.',
       '프로도와 네오는 연인이다.',
       '콘은 크로코다일과 콩알이 조합한 이름이다.',
       '무지는 토끼옷 입은 단무지이다.',
       '튜브는 소심한 오리이다.',
       '어피치는 유전자 변형으로 자웅동주가 된 것을 알고 복숭아 나무에서 탈출하였다.']

for i in text:
    if compile_val.search(i):
        print(i)
    else:
        print('FALSE')
#------------------
end = time.time()
elapsed = end - start
print(elapsed)
#------------------
0.0005469322204589844
```



```python
# 정규표현식 for문에 넣고 실행

import time
start = time.time()
#------------------
import re

text = ['라이언과 무지는 친구이다.',
       '라이언과 콘도 친구이다.',
       '프로도와 네오는 연인이다.',
       '콘은 크로코다일과 콩알이 조합한 이름이다.',
       '무지는 토끼옷 입은 단무지이다.',
       '튜브는 소심한 오리이다.',
       '어피치는 유전자 변형으로 자웅동주가 된 것을 알고 복숭아 나무에서 탈출하였다.']

for i in text:
    if re.compile(r'라이언|무지|콘').search(i):
        print(i)
    else:
        print('FALSE')
#------------------
end = time.time()
elapsed = end - start
print(elapsed)
#------------------
0.0007700920104980469
```





#### `re.match` 이용

`re.search` 는 포함관계에 있으면 True를 반환한다.

`re.match` 는 공백 기준으로 완벽하게 일치해야 True를 반환한다.

```python
import re

compile_val = re.compile(r'라이언|무지|콘')
text = ['라이언',
        '라이어',
        '모지',
        '무지는 무지',
        '라무지언'
       '라이언 무지',
       '라이언무지',
       '콘 무지',
       '라이언무지콘',
       '라이언콘무지',
       '라이언 콘 무지',
       '어피치 프로도',
       '제이지 라이',
       '어피치 네오']

for i in text:
    if compile_val.match(i):
        print(i)
    else:
        print('FALSE')
----------------------------------
라이언
FALSE
FALSE
무지는 무지
FALSE
라이언무지
콘 무지
라이언무지콘
라이언콘무지
라이언 콘 무지
FALSE
FALSE
FALSE
```

* `라무지언` 의 경우 `무지`, `라이언` 과 정확하게 일치 하지 않으므로 FALSE가 반환된다. 앞에서 부터 매칭 시키기 때문에 중간에 `무지` 가 있어도 FALSE가 반환되는 것이다.

