---
date: 2018-04-02
title: "[Programming] Python에서 CSV 파일을 읽어들이는 여러가지 방법"
excerpt: "Python에서 CSV 파일을 읽어들이는 여러가지 방법을 간결하게 정리"
categories: programming
comments: true
---



## 방법1. 기본 내장함수 사용

### 1. csv.reader

```python
import csv
dat = open('file.csv')
reader = csv.reader(dat)
lines = list(reader)
```

<br>

### 2. 한 줄씩 읽어들여서 리스트로 만들기

```python
import csv
dat1_list = []
dat2_list = []

with open('file.csv', 'r') as raw:
    reader = csv.reader(raw)
    for lines in reader:
        print(lines)
        dat1_list.append(lines)
        start = len(dat2_list)
        dat2_list[start:start] = lines
```

<br>

### 3. from_csv

```python
dat.from_csv('file.csv',
          sep = ',',
          encoding = 'utf-8')
dat.head()
```

<br>

### 4. readlines()

```python
open('file.csv').readlines()    # 파일을 한 줄씩 전체를 읽어들여서 리스트로 반환
```

<br><br><br>

## 방법2. Pandas 사용

```python
import pandas as pd
dat = pd.read_csv('file.csv', 
                  thousands = ',',
                  index_col = 0,
                  names = ['col1', 'col2', 'col3'],
                  encoding = 'utf-8')

dat.head()

dat.columns    # 열 이름 출력
dat.rename(columns = {dat.columns[0] : '명칭'}, inplace = True )    # 열 이름 변경
```



