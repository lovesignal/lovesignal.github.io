---
layout: post
date: 2018-04-05
title: Python & Django Day2
tags: [django, python]
categories: programming
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>

## Type과 연산(Numbers, String, boolean)

### Built-In Function
* type()
Numbers - int, float
Strings
Boolean

* var = input(‘입력’)

* int(), float(), str()

* String format 💡
```
"안녕하세요 %s씨, %d년 새해 복 많이 받으세요."%("현솔", 2018)

"안녕하세요 {name}씨, 오늘은 {day}입니다.".format(name="현솔", day="월요일")
```

* len()

<br>

<br>

### String

```
string = "Python"
string[0]

string = input("좋아하는 프로그래밍 언어를 입력하세요. :")
string[len(string)-1]
string[-1]
```

<br>

### Slice

[start : end : step(optional)] 
```
string = "I love python"
string[::2]
string[:]
string[:len("python")]
string[:-1]
```

<br>

### Immutable

* mutable vs immutable


![](https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_immutable.png)

<Br>

<br>



## Data Structure
### List
```
likes = []
likes.append("치킨")
likes.append("고양이")
likes.append("씨리얼")

print(likes)
```

<Br>

### del

```
del var[0]
```

<br>

### reverse()

```
var = [1,2,3,4,5,6,7]
var.reverse()
print(var)
# [7, 6, 5, 4, 3, 2, 1]
```

<br>

### sort()

```
numbers = [1,9,2,3,5,6,7,8,4]
numbers.sort()
print(numbers)
```

<br>

### pop()

```
numbers = [1,2,3,4,5]
a = numbers.pop(0)
print(a)
# 1
```

✏️ del 과 pop 차이점 생각하기

<br>

### insert()

* 값을 삽입
* 기존 값 있을 경우 덮어쓰기

```
numbers = [1, 2, 3, 4, 5]
numbers.insert(0, 0)    # 0번째에 0 넣음
print(numbers)
# [0, 1, 2, 3, 4, 5]
```

<br>

### extend()

* 더하기 연산자와의 차이 생각
* 기존 변수에 확장됨. 값 변함.
```
numbers = [1, 2, 3, 4, 5]
numbers2 = [6, 7, 8]
numbers.extend(numbers2)
pirnt(numbers)
# [1, 2, 3, 4, 5, 6, 7, 8]
```

<br>

### count()

```
numbers = [1, 2, 3, 3, 3, 4, 5, 6, 7, 7]
numbers.count(3)
# 3
```

<br>

### remove()

```
numbers = [1, 2, 3, 3, 3, 4, 5, 6, 7, 7]
numbers.remove(1)
# 1번째 값 삭제 됨

del numbers[1]
```

<br><br>




## List 복사
* 파이썬은 모든 값들이 객체

![](https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_list1.png)

![](https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_list2.png)



<br>

### copy()
```
>>> a = [1, 2, 3, 4, 5]
>>> b = a.copy()
>>> a.append(6)
>>> print(a)
[1, 2, 3, 4, 5, 6]
>>> print(b)
[1, 2, 3, 4, 5]
>>>
```

<br>

### Type : Boolean

True, False 값
