---
key: 20180822
title: "[Data Structure] Graph"
excerpt: "그래프 자료구조 이해 및 구현"
tags: algorithms, data structure
---



## 정의

네트워크 구조를 추상화한 모델. 간선(edge)으로 연결된 노드(node)의 집합이다. 

그래프에 대한 설명과 구현은 이 곳에 잘 나와있다.

http://blog.benoitvallon.com/data-structures-in-javascript/the-graph-data-structure/

<br>

그래프의 용어를 그림 하나로 정리해보면 아래와 같다.

<img src="https://github.com/lifeisgouda/img/blob/master/Algorithms/graph.png?raw=true">

<br>

동적 그래프 자료구조는 인접리스트(adjacency list)로 표현 가능하다.

위 그래프를 인접리스트로 나타낸 것이다.

> A : B C D
>
> B : A E F
>
> C : A D G
>
> D : A C G H
>
> E : B I
>
> G : C D
>
> H : D
>
> I : E

<br>

## Graph Class 구현하기

```javascript
let Dictionary = function Dictionary(){ let items = {}; }

function Graph(){
    let verices = []; // 정점은 배열로 저장
    let adjList = new Dictionary(); 
    // 인접리스트는 딕셔너리로 저장. 정점 이름이 key, 정점 리스트가 value.
    
    /* 정점 추가하는 메서드 구현*/
    this.addVertex = function(V) {
        vertices.push(v);   // 인자를 v에 받아서 verices 배열에 넣는다.
        adjList.set(v, []); // key가 v이고 값은 빈 배열인 딕셔너리를 인접 리스트로 세팅한다.
    };
    
    /* 간선을 추가하는 메서드 구현 */
    this.addEdge = function(v, w) {
        adjList.get(v).push(w);  
        // v, w를 인자로 받아서 w를 v의 인접리스트에 넣고 v -> w 방향의 간선을 추가한다.
        adjList.get(w).push(v); 
        // 무방향 그래프를 만들기 위해 w -> v 간선도 추가한다.
        
        // get()은 mapObj.get(key) 형태로 사용하는데 key와 연결된 value를 반환한다.
    };
    
    /* 인접 리스트를 문자열로 바꾸기 */
    this.toString = function() {
        let s = '';
        for (let i = 0; i < vertices.length; i++) {
            s += vertices[i] + ' -> ';
            let neighbors = adjList.get(vertices[i]);
            for (let j = 0; j < neighbors.length; j++) {
                s += neighbors[j] + ' ';
            }
            s += '\n';
        }
        return s;
    }
}

```



테스트 : 

```javascript
let graph = new Graph();
let myVertices = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I'];
for (let i = 0; i < myVertices.length; i++){
    graph.addVertex(myVertices[i]);
}

graph.addEdge('A', 'B');
graph.addEdge('A', 'C');
graph.addEdge('A', 'D');
graph.addEdge('C', 'D');
graph.addEdge('C', 'G');
graph.addEdge('D', 'G');
graph.addEdge('D', 'H');
graph.addEdge('B', 'E');
graph.addEdge('B', 'F');
graph.addEdge('E', 'I');

console.log(graph.toString());

/* 출력 결과 */
A -> B C D 
B -> A E F 
C -> A D G 
D -> A C G H 
E -> B I 
F -> B 
G -> C D 
H -> D 
I -> E 
```





