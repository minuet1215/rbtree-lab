# RB Tree 삭제

## 삭제 overview
1. 삭제 전 RB 트리 속성은 만족한 상태
2. 삭제 방식은 일반적인 BST와 동일
3. 삭제 후 RB 트리 속성 위반 여부 확인
4. RB 트리 속성을 위반했다면 재조정
5. RB 트리 속성을 다시 만족

## 삭제되는 색을 통해 색상 위반 여부 확인
1. 삭제하려는 노드의 자녀가 없거나 하나라면 삭제되는 색 = 삭제되는 노드의 색
2. 삭제하려는 노드의 자녀가 둘이라면 삭제되는 색 = 삭제되는 노드의 successor의 색
* 유효한 값을 가지는 자녀를 의미

- 삭제되는 색이 red라면 어떠한 속성도 위반하지 않는다.
- 삭제되는 색이 black이라면 2, 4, 5 속성을 위반할 수 있다.

## extra black의 역할
- 삭제되는 색이 black이고 속성을 위반할 때,
- 경로에서 black 수를 카운트 할 때 extra black은 하나의 black으로 카운트 된다.
- **doubly black** : extra black이 부여된 black 노드
- **red-and-black** : extra black이 부여된 red 노드 -> black으로 바꾸면 해결

## doubly black에서 extra black을 없애는 4가지 Case
1. doubly black의 오른쪽 형제가 black이고 그 형제의 오른쪽 자녀가 red 일 때,
<br>```- 그 red를 doubly black 위로 옮기고, 옮긴 red로 extra black을 전달해서 red-and-black으로 만들면 red-and-black을 black으로 바꿔서 해결```
<br>```- 오른쪽 형제는 부모의 색으로, 오른쪽 형제의 오른쪽 자녀는 black으로, 부모는 black으로 바꾼 후에, 부모를 기준으로 왼쪽(오른쪽)으로 회전하면 해결```

2. doubly black의 오른쪽 형제가 black이고, 그 형제의 왼쪽 자녀가 red, 오른쪽 자녀는 black 일 때,
<br>``` - doubly black의 형제의 오른쪽 자녀가 red가 되게 만듦```
<br>``` - doubly black의 오른쪽 형제의 오른쪽(왼쪽) 자녀를 red가 되게 만들어서 1번 케이스를 적용하여 해결red```

3. doubly black의 형제가 black이고, 그 형제의 두 자녀 모두 black일 때,
<br> ``` - doubly black과 그 형제의 black을 모아 부모에게 전달해서 부모가 extra black을 해결하도록 위임```
<br> ``` - 부모가 red-and-black이 됐다면 black 으로 변경하면 됨```
<br> ``` - 부모가 doubly black이 됐을때, 1) 루트 노드라면 black으로 바꿔서 해결, 2) 아니라면 case 1,2,3,4중 하나를 적용하여 해결``` 

4. doubly black의 형제가 red일 때
<br> ``` - doubly black의 형제를 black으로 만든 후 case 2,3,4 중 하나로 해결 ```
<br> ``` - 부모와 형제의 색을 바꾸고, 부모를 기준으로 왼쪽(오른쪽)으로 회전한 뒤 doubly black을 기준으로 case 2,3,4중 하나로 해결```
