# 알고리즘
## 합집합 찾기 (Union-Find)
- 그래프의 대표 알고리즘
- 서로소 집합 (Disjoint-Set) 알고리즘이라고도 불림
- 여러개의 노드가 존재할 때 두 개의 노드를 선택해서 현재 두 노드가 서로 같은 그래프에 속하는지 판별하는 알고리즘

### 합침 (Union)
- 각 노드가 자기 자신을 부모 노드로 하여 존재
- 서로 다른 두 노드가 합쳐질 때는 같은 부모 노드를 가지도록 함
- 일반적으로 부모 노드가 더 작은 값을 가지고 있는 쪽으로 합침

### 찾기 (Find)
- 두 개의 노드의 부모 노드를 확인하여 현재 같은 집합에 속하는지 확인하는 알고리즘
- 부모 노드가 같다면 같은 그래프안에 속하는 것으로 간주함

### 구현
```c#
using System;

// 합집합 알고리즘 - 서로소 알고리즘
// 그래프가 서로 연결되었는지 찾는 알고리즘

namespace Algorithm
{
    class Program
    {
        static void Main()
        {
            int[] parent = new int[11];
            for (int i = 1; i < parent.Length; i++)
            {
                parent[i] = i;
            }

            UnionParent(parent, 1, 2);
            UnionParent(parent, 2, 3);
            UnionParent(parent, 3, 4);
            UnionParent(parent, 5, 6);
            UnionParent(parent, 6, 7);
            UnionParent(parent, 7, 8);

            for (int i = 0; i < parent.Length; i++)
            {
                Console.WriteLine($"{i}: {parent[i]}");
            }
        }

        /// <summary>
        /// 부모 노드를 찾는 함수
        /// </summary>
        /// <param name="parent">부모 배열</param>
        /// <param name="x">찾는 노드 인덱스</param>
        /// <returns></returns>
        static int FindParent(int[] parent, int x)
        {
            // 부모 노드와 찾는 노드가 같다면 그대로 리턴
            if (parent[x] == x) return x;
            // 그렇지 않다면 부모 노드를 찾기 위해 재귀 수행
            return parent[x] = FindParent(parent, parent[x]);
        }

        /// <summary>
        /// 두 부모 노드를 합치는 함수
        /// </summary>
        /// <param name="parent">부모 배열</param>
        /// <param name="a">합칠 노드 인덱스</param>
        /// <param name="b">합칠 노드 인덱스</param>
        static void UnionParent(int[] parent, int a, int b)
        {
            a = FindParent(parent, a);
            b = FindParent(parent, b);

            // 부모 노드가 더 작은 값을 넣어준다.
            if (a < b) parent[b] = a;
            else parent[a] = b;
        }
    }
}
```