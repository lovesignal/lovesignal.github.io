---
key: 20180214
title: "[Data Structure] Circular Queue"
excerpt: "python3로 Circular Queue 구현하기"
comments: true
tags: [algorithms]
categories: algorithms
---

# python3로 Circular Queue 구현하기



## __ __init__ __()

먼저 데이터 구조의 초깃값을 정한다. Queue의 크기를 k로 두고, 값을 담을 수 있게 길이가 k인 리스트 `queue_list` 를 만든다.

Queue에는 두개의 포인터가 필요하다. 한개는 Front를 가리켜야 하고, 다른 하나는 Back을 가리켜야 한다.

<img src="https://i.imgur.com/VmtWFZV.png" width="500px">

```python
def __init__(self, k: int):
    self.size = 0    # 처음 리스트의 길이
    self.max_size = k    # 리스트의 길이
    self.queue_list = [0] * k   # Queue를 담을 리스트
    self.front = self.rear = -1    # pointer
```



## enQueue()

`enQueue()` 는 Circular Queue에 값을 삽입하는 함수이다.

`enQueue()` 는 boolean을 반환한다. 값을 삽입하는 것이 성공하면 `True` 를 반환하고, 실패하면 `False` 를 반환한다. 

1. 리스트의 초기 크기와 최대 크기가 같으면 값을 삽입할 수 없으므로 False를 반환한다.
2. 리스트의 뒷 부분(back)이 초기에 설정해둔 -1이면 `rear` 와 `front` 에 0을 넣는다. 왜냐하면 두 포인터 모두 리스트의 0번째 인덱스를 가리키고 있기 때문이다.
3. `rear` 값이 -1이 아니라면, `rear` 에 1을 증가 시키 것을 `max_size` 로 나머지 연산한 값이 `rear` 가 된다.
4. 그리고 `queue_list` 에서 `rear` 번째에 값이 들어간다.
5. 새 값이 들어가면서 길이가 증가하였으므로 `size` 를 1만큼 증가시킨다. 그리고 `True` 를 반환한다.

```python
def enQueue(self, value: int):
    if self.size == self.max_size:    # 1
        return False
    else:
        if self.rear == -1:    # 2
            self.rear = self.front = 0
        else:    # 3
            self.rear = (self.rear + 1) % self.max_size
        self.queue_list[self.rear] = value    # 4
        self.size += 1
        return True
```



## deQueue()

`deQueue()` 는 Circular Queue에 값을 삭제하는 함수이다.

`deQueue()` 는 boolean을 반환한다. 값을 제거하는게 성공하면 `True` 를 반환하고, 실패하면 `False` 를 반환한다.

```python
def deQueue(self):
        if self.size == 0: return False
        if self.front == self.rear:
            self.front = self.rear = -1
        else:
            self.front = (self.front + 1) % self.max_size
        self.size -= 1
        return True
```



## Front()

`Front()` 는 현재 start pointer가 가리키고 있는 값을 반환한다.

```python
def Front(self):
        return self.queue_list[self.front] if self.size != 0 else -1
```



## Rear()

`Rear()` 는 현재 end pointer가 가리키고 있는 값을 반환한다.

```python
def Rear(self) -> int:
        return self.queue_list[self.rear] if self.size != 0 else -1
```



## isEmpty()

`isEmpty()` 는 현재 값이 비어 있는지 아닌지 확인한다.

```python
def isEmpty(self) -> bool:
        return self.size == 0
```



## isFull()

`isFull()` 은 리스트에 값이 가득 차 있는지 아닌지 확인한다.

```python
def isFull(self):
        return self.size == self.max_size
```



## 전체 코드

```python

class MyCircularQueue:
    def __init__(self, k: int):
        self.size = 0
        self.max_size = k
        self.queue_list = [0] * k
        self.front = self.rear = -1

    def enQueue(self, value: int) -> bool:
        if self.size == self.max_size:
            return False
        else:
            if self.rear == -1:
                self.rear = self.front = 0
            else:
                self.rear = (self.rear + 1) % self.max_size
            self.queue_list[self.rear] = value
            self.size += 1
            return True

    def deQueue(self) -> bool:
        if self.size == 0: return False
        if self.front == self.rear:
            self.front = self.rear = -1
        else:
            self.front = (self.front + 1) % self.max_size
        self.size -= 1
        return True

    def Front(self) -> int:
        return self.queue_list[self.front] if self.size != 0 else -1

    def Rear(self) -> int:
        return self.queue_list[self.rear] if self.size != 0 else -1

    def isEmpty(self) -> bool:
        return self.size == 0

    def isFull(self) -> bool:
        return self.size == self.max_size
```

