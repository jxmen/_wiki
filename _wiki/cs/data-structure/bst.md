---
layout  : wiki
title   : Binary Search Tree 
summary : 
date    : 2024-03-26 16:12:07 +0900
updated : 2024-03-29 01:50:00 +0900
tag     : 
toc     : true
public  : true
parent  : [[/cs/data-structure]] 
latex   : false
resource: 2AE3383F-8DA3-4FC6-B46B-402E6521C752
---
* TOC
{:toc}

### BST(Binary Search Tree)란?

Binary Tree + 특정한 룰

- 왼쪽 SubTree는 반드시 지금 노드의 값보다 작은 값
- 오른쪽 SubTree는 반드시 지금 노드의 값보다 큰 값

예시

```
      5
     / \
    /   \
   3     7
  / \
 /   \
1     4
```

### BST의 시간복잡도

BST에서 어떤 값이 존재하는지 확인하기 위해서는, 트리의 **최대 깊이**만큼만 탐색해서 찾을 수 있다.

N개의 노드가 밸런싱되어 꽉찬 경우에도 시간복잡도는 `O(logN)`이 소요된다.

### 정렬된 배열에서도 Binary Search가 가능한데 BST를 쓰는 이유는?

이미 정렬된 배열이라도 사실 Binary Search 가 가능하다.

```
1 2 5 7 9 10 
```

하지만 배열은 삽입/삭제 등은 기존에 저장된 데이터를 밀어내는 과정이 추가로 필요하므로 `O(N)`의 시간복잡도를 가지게 된다.

BST는 삽입/삭제 역시 평균적으로 `O(logN)`만에 수행할 수 있기 때문에 효과적이다. 

### BST의 삭제

삭제의 경우가 조금 신경써야 할 부분이 있다. 삭제가 되었을때도 BST의 형태를 유지해야 한다.

자식이 없는 경우 - 삭제할 대상을 NULL로 변경하기만 하면 된다.
```
  50         50
 /  \   ->  /  \
30  70    NULL 70
```

자식이 하나만 있는 경우 - 삭제하려는 노드의 자식들을 부모의 자식으로 연결한다.

```
    50                    50
   /  \                  /  \
  30  70 (30 제거) ->   40   70
 /
40
```

자식이 둘 다 있는 경우 - 삭제하려는 대상의 오른쪽 자식에서 가장 작은 값으로 대체한다.

```
  50                  70
 /  \                /  \
30  80  (50 제거) -> 30  80
   /  \                   \
  70  90                  90
```

### Self-Balancing

극단적으로는 다음과 같은 형태도 BST에 속한다.

```
1
 \
  2
   \ 
    3...
```

트리의 깊이가 계속해서 깊어져 검색 효율이 좋지 못할 수 있다. 이를 방지하기 위해 밸런스를 알아서 잡는 트리들이 존재한다.

- AVL Tree
- Red-Black Tree

### AVL Tree

`balance factor`라는 것을 통해 스스로 균형을 유지한다. balance factor란 어떠한 노드의 왼쪽 서브트리와 오른쪽 서브트리의 값 차이를 말한다. 

모든 노드의 balance factor가 {-1, 0, 1}을 충족할 때 AVL Tree가 된다. 밸런스 팩터 체크는 트리의 삽입 혹은 삭제 후 균형을 맞추는 작업을 진행하게 된다.

```
50           
 \          70
  70  ->   /  \
   \      50  90
    90
```

balance factor 동작 시 AVL Tree를 만족하면서도 BST를 만족해야 한다. 예를 들어 오른쪽-왼쪽으로 꺾인 트리의 경우는 다음 과정을 통해 균형을 맞추게 된다.

```
50      50       
 \       \          60
 70 ->   60  ->    /  \
 /        \       50  70
60        70
```

AVL Tree는 밸런스를 스스로 잡게 되므로, 기존 BST 최악의 경우 `O(N)`의 시간복잡도를 `O(logN)`으로 개선한다. 다만 밸런스 팩터 동작 과정에서 루트 노드까지 탐색을 하는 과정이 있어 이러한 시간이 걸리는 것도 고려해야 한다.

### Red-Black Tree

root 노드 black부터 시작하여 black의 자식은 red, 그 자식은 다시 black 번갈아가면서 트리 형태를 유지하는 BST의 일종이다. NULL 대신 nill 노드를 사용한다는 특징이 있다.

![red-black tree]( /resource//0ccc3561-9cfe-4d06-8429-c0d6c7a19aa5.png )

### 참고자료

- [코맹탈출 - 자료구조 Binary Search Tree](https://www.youtube.com/watch?v=wQwB5gdnEDg)
- [쉬운코드 - AVL 트리](https://www.youtube.com/watch?v=syGPNOhsnI4)

### 각주
[^1]: 교과서적인 용어로는 `rotate`라고 한다.
