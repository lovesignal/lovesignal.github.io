---
layout: post
date: 2018-02-19
title: "[R] R의 Data Structure"
excerpt: "R의 기본적인 데이터 구조 설명"
categories: Statistics
comments: true
tags: [R, data structure]
comments: true
---

# [R] R의 Data structure

## 데이터 구조 종류

- **Scalar** : element가 1개인 vector이다. 

  ```r
  # scalar 만들기
  a <- 'a'
  alphabet <- 'abcdefg'
  num <- 1
  ```

  ​

- **Vector** : 같은 종류의 element가 여러개 들어 있는 1차원 matrix이다.

  ```r
  # vector 만들기
  table <- c('a', 'b')
  table <- c(1, 2, 3, 5)
  bool <- c(TRUE, FALSE)
  ```

  ​

- **Matrix** : 2차원으로 된 배열. 일반적이 표 데이터를 생각하면 된다.

  ```r
  # matrix 만들기
  # 2 by 3 행렬 생성
  > mat <- matrix(c("a", "b", "c", "d", "e", "f"), nrow = 2, ncol = 3)
  > mat
      [,1] [,2] [,3]
  [1,] "a"  "c"  "e" 
  [2,] "b"  "d"  "f" 

  ```

  ​

- **Array** : 차원이  matrix 보다 많다. Matrix는 2차원(행, 열)인데 비해 배열은 그 이상 차원이 형성될 수 있다.

  ```r
  # array 만들기
  > animal <- c("dog", "cat", "rabbit")
  > feed <- c("meat", "fish", "carrot")
  > jump <- c("3", "2", "1")
  > arr <- array(data = c(animal, feed, jump), dim = c(1,3,3), dimnames = list('value', c(1, 2, 3), c('animal','feed','jump')))

  # array(c(vector1, vector2, vector3), dim = c(1,3,3), dimnames = list(row.names, column.names, matrix.names))

  > arr
  , , animal

        1     2     3       
  value "dog" "cat" "rabbit"

  , , feed

        1      2      3       
  value "meat" "fish" "carrot"

  , , jump

        1   2   3  
  value "3" "2" "1" 

  ```

  ![](https://lovesignal.github.io/img/post/Study/R_1.png)



- **Data Frame** : matrix와 유사한데, 유형이 다른 데이터를 함께 넣을 수 있다.

  ```R
  > animal <- c("dog", "cat", "rabbit")
  > feed <- c("meat", "fish", "carrot")
  > jump <- c("3", "2", "1")
  > dat <- data.frame(animal, feed, jump)
  > dat
    animal   feed jump
  1    dog   meat    3
  2    cat   fish    2
  3 rabbit carrot    1
  ```

  ​


- **List** :서열화된 성분들의 집합체이다. 예시를 보는 게 빠르다.

  ```R
  > title <- "Phone Book"
  > name <- c("Tom", "Jack", "Jean", "Mike")
  > phone <- c("010-1234-1234", "010-2345-5678", "010-9876-5673")
  > index <- c(1, 2, 3)
  > etc <- matrix(1:10, nrow=2)

  > mylist <-list(title = title, info = name, phone, index, etc)
  > mylist
  $title
  [1] "Phone Book"

  $info
  [1] "Tom"  "Jack" "Jean" "Mike"

  [[3]]
  [1] "010-1234-1234" "010-2345-5678" "010-9876-5673"

  [[4]]
  [1] 1 2 3

  [[5]]
       [,1] [,2] [,3] [,4] [,5]
  [1,]    1    3    5    7    9
  [2,]    2    4    6    8   10

  > mylist$title
  [1] "Phone Book"

  > mylist[[3]]
  [1] "010-1234-1234" "010-2345-5678" "010-9876-5673"

  > mylist$info[1]
  [1] "Tom"
  ```

  ​

