---
key: 20190319
title: "[python] Pandas를 이용한 데이터 전처리 2"
excerpt: "pandas를 이용하여 특정 단어가 포함 되었는지 확인하는 방법"
categories: programming
comments: true
tag : [programming, python, pandas]
---

## The efficient way to loop through data frames with Pandas

먼저 데이터 프레임을 만든다.

```python
import pandas as pd

member = ['라이언', '무지', '콘', '프로도', '제이지', '네오', '어피치']
weight = ['30', '25', '5', '20', '25', '15', '20']
age = ['5', '4', '10', '3', '7', '6', '11']

kakao_friends = pd.DataFrame()
kakao_friends['member'] = member
kakao_friends['weight'] = weight
kakao_friends['age'] = age
```

|      | member | weight | age  |
| ---- | ------ | ------ | ---- |
| 0    | 라이언 | 30     | 5    |
| 1    | 무지   | 25     | 4    |
| 2    | 콘     | 5      | 10   |
| 3    | 프로도 | 20     | 3    |
| 4    | 제이지 | 25     | 7    |
| 5    | 네오   | 15     | 6    |
| 6    | 어피치 | 20     | 11   |



### 1. `iterrows`

첫번째 변수`idx` 에 인덱스를 받고,  member는 member 열의 행에 하나씩 접근하여 출력한다.

```python
# Iterate over rows of kako friends
for idx, member in kakao_friends.iterrows():
    print(idx, member)
-------------------------
0 member    라이언
weight     30
age         5
Name: 0, dtype: object
1 member    무지
weight    25
age        4
Name: 1, dtype: object
2 member     콘
weight     5
age       10
Name: 2, dtype: object
3 member    프로도
weight     20
age         3
Name: 3, dtype: object
4 member    제이지
weight     25
age         7
Name: 4, dtype: object
5 member    네오
weight    15
age        6
Name: 5, dtype: object
6 member    어피치
weight     20
age        11
Name: 6, dtype: object
```



아래와 같이 입력해도 결과는 동일하다.

```python
# 1
for member, row in kakao_friends.iterrows():
    print(member, row)

# 2    
for weight, row in kakao_friends.iterrows():
    print(weight, row)
    
# 3
for age, row in kakao_friends.iterrows():
    print(age, row)
```



```python
# 4: 아래과 같이 출력할 수도 있다.
for index, row in kakao_friends.iterrows():
    print(row["member"], row["age"])
---------------- 
라이언 5
무지 4
콘 10
프로도 3
제이지 7
네오 6
어피치 11
```





### 2. `itertuples`

```python
for row in kakao_friends.itertuples(index=True):
    print(getattr(row, "member"), getattr(row, "age"))
    
-----------
라이언 5
무지 4
콘 10
프로도 3
제이지 7
네오 6
어피치 11
```



* `itertuples()` is supposed to be faster than `iterrows()` .

* `itertuples` 사용에 있어서 주의할 점이 있다. 공식문서에서 아래와 같이 밝히고 있다.

  > According to the docs (pandas 0.21.1 at the moment):
  >
  >- iterrows: `dtype` might not match from row to row
  >
  >  > Because iterrows returns a Series for each row, it **does not preserve**dtypes across the rows (dtypes are preserved across columns for DataFrames).
  >
  >- iterrows: Do not modify rows
  >
  >  > You should **never modify** something you are iterating over. This is not guaranteed to work in all cases. Depending on the data types, the iterator returns a copy and not a view, and writing to it will have no effect.
  >
  >  Use [DataFrame.apply()](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html) instead:
  >
  >  ```
  >  new_df = df.apply(lambda x: x * 2)
  >  ```
  >
  >- itertuples:
  >
  >  > The column names will be renamed to positional names if they are invalid Python identifiers, repeated, or start with an underscore. With a large number of columns (>255), regular tuples are returned.
  >
  >





### 3. `zip` 과 `enumerate` 사용

```python
for index, (member, age) in enumerate(zip(kakao_friends['member'], kakao_friends['age'])):
    print(index, member, age)
-----------------
0 라이언 5
1 무지 4
2 콘 10
3 프로도 3
4 제이지 7
5 네오 6
6 어피치 11
```





### 추천하지 않는 방법

```python
for i in range(len(kakao_friends['member'])):
    print(kakao_friends['member'][i])
-------------------
라이언
무지
콘
프로도
제이지
네오
어피치
```



```python
%%timeit
for i in range(len(kakao_friends['member'])):
    print(kakao_friends['member'][i])
843 µs ± 14.1 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)


%%timeit
for i in kakao_friends['member']:
    print(i)
742 µs ± 8.22 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```

>### Crude looping in Pandas, or That Thing You Should Never Ever Do
>
>To start, let’s quickly review the fundamentals of Pandas data structures. The basic Pandas structures come in two flavors: a **DataFrame** and a **Series**. A DataFrame is a two-dimensional **array** with labeled axes. In other words, a DataFrame is a matrix of rows and columns that have labels — column names for columns, and index labels for rows. A single column or row in a Pandas DataFrame is a Pandas series — a one-dimensional array with axis labels.
>
>Just about every Pandas beginner I’ve ever worked with (including yours truly) has, at some point, attempted to apply a custom function by looping over DataFrame rows one at a time. The advantage of this approach is that it is consistent with the way one would interact with other iterable Python objects; for example, the way one might loop through a list or a tuple. Conversely, the downside is that a crude loop, in Pandas, is the slowest way to get anything done. Unlike the approaches we will discuss below, crude looping in Pandas does not take advantage of any built-in optimizations, making it extremely inefficient (and often much less readable) by comparison.
>
>[출처]: https://engineering.upside.com/a-beginners-guide-to-optimizing-pandas-code-for-speed-c09ef2c6a4d6	"A Beginner’s Guide to Optimizing Pandas Code for Speed"



* 참고 글 : https://aldente0630.github.io/data-science/2018/08/05/a-beginners-guide-to-optimizing-pandas-code-for-speed.html