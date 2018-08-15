---
date: 2018-06-04
layout : post
title: "[Algorithms] Harmless Ransom Note in Javascript"
excerpt: "Harmless Ransom Note를 이해하고 javascript로 풀기. hash table을 이용하여 객체를 다루고 빠른 프로그램 구현하는 것이 목표."
comments: true
tags: [algorithms]
use_math: true
categories: algorithms
---



## 문제

Harmless ransom note algorithm은 두개의 parameter를 갖는다.

첫번째 parameter인 noteText는 string과 같은 텍스트를 받을 수 있다. 두번째 parameter인 magazineText에도 string 같은 텍스트가 들어간다. 

예를들어, 아래와 같이 note와 meagazine이 쓰여있다

> Note : 'this si a **secret** note for you from a **secret** admirer.'

> Magazine : 'puerto rico is a great place you must hike far from town to find a **secret** waterfall that i am an admirer of but note that it is not as hard it seems this my advice for you'

입력받은 두개의 파라미터 텍스트를 비교해서 중복되는 text(문자열)이 있으면 true를 반환하고, 없으면 false를 반환한다. 예시를 보면, Note의 secret과 Magazine의 secret이 중복되므로 true를 반환하게 된다.

```javascript
function harmlessRansomeNote(noteText, magazineText) {
    
}
```

<br>

<br>

## Big O

Big O(빅오)는 알고리즘이나 함수를 측정 및 분류하기 위해 사용된다. bigO는 worst case의 알고리즘 실행시간이나 입력 크기에 기반하여 알고리즘 수행시간이 얼마나 긴지 추정한다.

<br>

### Constant runtime

아래 log function이 정의되어 있다. 이 함수는 array를 입력 값으로 받고, 첫번째와 두번째 element를 프린트한다. 이 함수의 bigO는 상수일 것이다. 이 함수는 입력 크기가 증가하더라도 첫번째와 두번째 값을 출력하는 수행하는 것은 바뀌지 않는다. 그러므로 실행시간이 상수이고 bigO 역시 상수이다.

실행시간이 상수인 경우 bigO는 0 또는 1로 쓴다.

```javascript
function log(array) {        // BigO Notation : "O(1)"
    console.log(array[0]);   
    console.log(array[1]);
}

log([1, 2, 3, 4]);
log([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
```

<br> 

<img src="https://www.packtpub.com/graphics/9781783988181/graphics/8181_02_05.jpg">

<br><br>

### Linear runtime

logAll 함수는 array를 인자로 받아서 모든 값을 출력한다. 이 함수의 경우 입력 크기가 증가하면 실행시간도 증가한다. 즉, 입력크기와 실행시간이 선형관계이다. 이 경우 bigO는 O(n)으로 표기한다. 입력크기 n에 비례하여 실행시간이 증가하는 것이다.

```javascript
function logAll(array) {   // Linear runtime
                           // Big O Notation: "O(n)"
    for (let i = 0; i <array.length; i++) {
        console.log(array[i]);
    }
}

logAll([1, 2, 3, 4, 5]);
logAll([1, 2, 3, 4, 5, 6])
logAll([1, 2, 3, 4, 5, 6, 7]);
```

<br><br>

### Exponenetial runtime

addAndLog 함수는 두개의 반복구간이 있다. 이 경수 요소가 3개인 array를 입력값으로 받으면 $$3^2$$ 번 계산하게 되고, 요소가 4개인 array를 입력값으로 받으면 $$4^2$$번 연산하게 된다. 5개 요소의 경우 $$5^2$$번 연산한다. 즉, 실행시간이 지수적으로 증가(exponenetial jump) 하게 된다. 실행시간이 지수인 경우 bigO는 $$O(n^2)$$ 이 된다.

```javascript
function addAndLog(array) { // Exponential runtime
                            // Big O Notation: "O(n^2)"
    for (let i = 0; i < array.length; i++) {
        for (let j = 0; j < array.length; j++) {
            console.log(array[i] + array[j]);
        }
    }
}

addAndLog(['A', 'B', 'C']);     // 9 pairs logged out
addAndLog(['A', 'B', 'C', 'D']);    // 16 pairs logged out
addAndLog(['A', 'B', 'C', 'D', 'E'])    // 25 pairs logged out
```

<br><br>

### Logarithmic runtime

실행시간이 로그함수인 코드는 성능이 매우 좋다. 아래 코드의 이진 탐색 알고리즘(binary search algorithm)은 두개의 값을 받는다. array는 오름차순 정렬된 리스트이고, 다른 하나 key는 한개의 값이다. array에서 key와 일치하는 값을 찾는 탐색이다. 이진 탐색 알고리즘의 실행시간은 로그함수를 따른다. 큰 사이즈의 문제를 일정 크기의 작은 문제로 쪼개서 연산하므로 효율성이 높은 탐색이 가능하다. 4000개의 요소를 탐색하는데 최대 12번의 연산이면 된다.

```javascript
function binarySearch(array, key) {    // Logarithmic runtime
    let low = 0;                       // Big O Notation: "O(logn)
    let high = array.length - 1;
    let mid;
    let element;
    
    while (low <= high) {
        mid = Math.floor((low + high) / 2, 10);
        element = array[mid];
        if (element < key) {
            low = mid + 1;
        } else if (element > key) {
            high = mid - 1;
        } else {
            return mid;
        }
    }
}
```

<br>

<br>

<br>

## Harmless Ransom Note Code

### Code 1.

- Assume : NoteText and magazineText do not contain any type of puctuation and all the letters are lowercase.

먼저, noteText와 magazineText에 입력받은 문자열을 각각 단어 array로 바꿔야 한다. 공백을 기준으로 나눠서 array에 저장한다. 

```javascript
function harmlessRansomNote (noteText, magazineText) {
    let noteArr = noteText.split(' ');
    let magazineArr = magazineText.split(' ');
}
```

<br>

one array로 저장되어 있으므로 hash table로 저장할 수 있게 빈 객체를 생성한다.

```javascript
function harmlessRansomNote (noteText, magazineText) {
    let noteArr = noteText.split(' ');
    let magazineArr = magazineText.split(' ');
    let magazineObj = {};
}
```

<br>

<br>

### forEach()

`forEach()` 메소드는 배열 요소마다 한 번씩, 제공한 함수를 실행한다. (*참고 : <a href="https://msdn.microsoft.com/ko-kr/library/ff679980(v=vs.94).aspx">forEach 메서드(Array)</a>)

forEach 메서드는 아래와 같은 syntax를 갖는다.

```javascript
arr.forEach(function callback(currentValue[, index[, array]]) {
    //your iterator
}[, thisArg]);
```

callback은 각 요소마다 실행될 함수이다.

currentValue는 배열에서 현재 처리 중인 요소이다.

index는 배열에서 현재 처리 중인 요소의 인덱스이다.

array는 `forEach()`가 적용되고 있는 배열이다.

`thisArg` 는선택 사항.  `callback`을 실행할 때 `this`로서 사용하는 값이다.

 <br>

간단하게 배열 각 요소에 10을 곱해주는 forEach()를 구현한 것이다.

arr이 적용될 array이다. 함수에 3가지 인자를 받고 있는데 위 sytax와 비교해보면 x는 currentValue, index는 index, array는 array이다.

```javascript
let arr = [1, 2, 3, 4, 5]
arr.forEach(function (x, index, array){
   array[index] = x * 10; 
});
console.log(arr)    // [ 10, 20, 30, 40, 50 ]
```

<br>

화살표 함수로 간단하게 구현하면 아래와 같다.

```javascript
let arr = [1, 2, 3, 4, 5];
let result = [];
arr.forEach(x => { result.push(x * 10) });
console.log(result);
```

<br><br>

forEach 메소드를 Harless Ransom Note 알고리즘에 적용한다. 단어가 저장되어 있는 배열을 각각 분리해서 빈 객체에 넣은 후 갯수를 카운팅 해주는 함수에 적용할 것이다.

```javascript
function harmlessRansomNote (noteText, magazineText) {
    let noteArr = noteText.split(' ');
    let magazineArr = magazineText.split(' ');
    let magazineObj = {};
    
    magazineArr.forEach(word => {
        if (!magazineObj[word]) magazineObj[word] = 0;
        magzineObj[word]++;
    });
    
    console.log(magazienObj);
}

harmlessRansomNote('', 'this is all the magazine text in the magazine');
// { this: 1, is: 1, all: 1, the: 2, magazine: 2, text: 1, in: 1 }
```

<br>

<br>

### Code 2.

`magazine`에 `note` 의 단어를 가지고 있는지 `noteArr`의 모든 단어를 반복해서 살펴 본다.

`noteArr` 배열을 반복하면서, 각 단어에 대해  `magazine`에 단어가 있는지 확인한다.  

적절한 단어가 없기 때문에 ransom note를 기록 할 수 없다는 것을 알고 있다. 

<br>

첫 번째로 `magazine` 에 있는 단어로  `note` 가 작성될 수 있는지 boolean 값을 얻는 것이다. 그러므로 초깃값이 true인 변수를 만든다. 

```javascript
let noteIsPossible = true
```

<br>

 그런 다음 `noteArr` 를 반복하면서 변수를 표시한다.

 `note` 는 `note` 를 작성하는 데 필요한 단어가 전혀 없는 경우 `false` 가 된다.

 그러므로 `note` 가 어딘가에 없다면이 변수를 `false` 를 반환한다.

코드 블록 내부에 `magazineObj` 에 단어가있는 경우 현재 단어를 넘긴 후 빼준다.(?)

```javascript
noteArr.forEach(word => {
	if (magazineObj[word]) {
		magazineObj[word]--;
	}
```

<br>

 `noteArr` 의 현재 단어가 `magazineObj` 에 없다면 `NoteIsPossible` 을 `false` 로 설정한다.

```javascript
	else noteIsPossible = false;
```



단어가 `magazineObj` 에 존재하면 단어 수를 감소시킨 후에 다른 IF 문을 넣는다.  `magazine의 단어수` 가 0보다 작으면 `noteIsPossible` 에  `false` 를 반환한다.

```javascript
if (magazineObj[word] < 0) noteIsPossible = false;
```

<br>

<br>

### 결과 코드

```javascript
function harmlessRansomNote (noteText, magazineText) {
    let noteArr = noteText.split(' ');
    let magazineArr = magazineText.split(' ');
    let magazineObj = {};

    magazineArr.forEach(word => {
        if (!magazineObj[word]) magazineObj[word] = 0;
        magazineObj[word]++;
    });

    let noteIsPossible = true;
    noteArr.forEach(word => {
        if (magazineObj[word]) {
            magazineObj[word]--;
            if (magazineObj[word] < 0) noteIsPossible = false;
        }
        else noteIsPossible = false;
    });

    return noteIsPossible;
}
```

<br>

<br>

## Time complex

Harmless Ransom Note 알고리즘은 시간복잡도가 O(n)이다. 

함수 안에 두 개의 반복문(loop)이 있고 중첩되지 않는다. 그러므로 시간복잡도는 exponential이 아니다. 

위 함수에서 시간 복잡도를 결정하는 가장 중요한 부분은 두 개의 루프이다.

<br>

- 첫 번째 루프 

  ```javascript
  magazineArr.forEach(word => {
  	if (!magazineObj[word]) magazineObj[word] = 0;
  		magazineObj[word]++;
  });
  ```

<br>

- 두번째 루프

- ```javascript
  noteArr.forEach(word => {
      if (magazineObj[word]) {
          magazineObj[word]--;
  		if (magazineObj[word] < 0) noteIsPossible = false;
      }
  	else noteIsPossible = false;
  });
  ```

<br>

이 두 루프는 서로의 내부에 중첩되어 있지 않기 때문에 선형 시간 복잡도 O(n)으로 실행된다. 이 경우 n은 몇개의 요소가 noteArray에 있는지 나타낸다.

첫번째, 두번째 루프 둘다 선형시간복잡도로 실행된다. 그러나 각각의 루프는 다른 array와 variable을 갖는다. 그러므로 **Linear Time Complexity는 O(n) + O(m) = O(n + m)**이다. 이런 경우 시간복잡도 O(n) 또는 O(n+m)으로 나타낼 수 있다. 





