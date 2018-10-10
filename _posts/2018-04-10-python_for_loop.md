---
key: 20180410
title: "[python] 리스트 변수를 반복문 돌리기 예시"
excerpt: "python에서 리스트 변수에 반복문을 사용하는 방법에 대한 예시"
categories: programming
comments: true
tag : [programming, python]
---



```python
students = []
student1_info = {
    "first_name": "Martin",
    "las_name" : "Lawrence",
    "student_no": 9854

}

student2_info = {
    "first_name": "Robert",
    "las_name" : "Gant",
    "student_no": 6790

}

student3_info = {
    "first_name": "George",
    "las_name" : "Murphy",
    "student_no": 4728

}

for i in range(1, 4):
    students.append(eval('student%d_info'% (i)))

print(students)

```



* `eval()` : 실행 가능한 문자열을 입력 받아 실행한 결과값을 리턴하는 함수이다.

  ```python
  >>> eval('1+2')
  3
  >>> eval("'hi' + 'a'")
  'hia'
  >>> eval('divmod(4, 3)')
  (1, 1)
  ```

  ​

* `append()` : 객체를 맨 뒤에 추가해주는 함수이다.

  ```python
  >>> x = [1, 2, 3]
  >>> x.append([4, 5, 6])
  >>> print (x)
  [1, 2, 3, [4, 5, 6]]
  ```

  ​


*  `extend()` : 여러개의 값을 확장시킬 수 있는 함수이다. 함수로 전달되는 인수에는 리스트만 올 수 있다.

  ```python
  >>> x = [1, 2, 3]
  >>> x.extend([4, 5, 6])
  >>> print (x)
  [1, 2, 3, 4, 5, 6]
  ```

  ​

