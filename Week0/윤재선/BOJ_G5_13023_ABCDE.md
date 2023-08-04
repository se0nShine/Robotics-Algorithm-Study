# BOJ_G5_13023_ABCDE[2023.08.04] </br>

## 알고리즘 종류
```
그래프 이론
그래프 탐색
깊이 우선 탐색
백트래킹
```

## 해설 및 느낀점
```
count를 초기화 하는 방식이 이상했다.. 매개변수로 안하고 전역변수로 하니까 이상하게 됬다. 
count값을 중간에 유지 해야된다면..? >> 함수의 매개변수로 넣는기 좋다. 
backtracking은 이번에 공부하면서 처음 알게 되었다.. 현재 상태까지 온걸 유지하면서 다음 것들을 확인해보는법? 이라고 이해하면 좋을거 같다. 
백트래킹에 대해서 더 공부해야겠다. 
그리고 재귀함수도 공부해야한다. 
계속 시간 초과가 나서.. 봤더니 재귀함수에서 return을 안써서 중간에 탈출을 안했다. 재귀함수도 복습 좀 해야겠다..
```
## 코드
```c++

#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> graph;
vector<bool> visited;
int num;
int  n,m;
bool flag=false;
void DFS(int vertex,int cnt)
{
    if(cnt>=4)
    {
        flag=true;
        return;
    }
    for(int j=0;j<graph[vertex].size();j++)
    {
        int curr_v=graph[vertex][j];
        if(!visited[curr_v])
        {
            visited[curr_v]=true;
            DFS(curr_v,cnt+1);
            visited[curr_v]=false;
        }
    }
}

int main()
{
    cin>>n>>m;
    graph.resize(n);
    visited.resize(n);
    for(int i=0;i<m;i++)
    {
        int y,x;
        cin>>y>>x;
        graph[y].emplace_back(x);
        graph[x].emplace_back(y);
    }
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<visited.size();j++)
        {
            visited[j]=false;
        }
        num=0;
        visited[i]=true;
        DFS(i,num);
        if(flag)
            break;
    }
    if(flag)
        cout<<1<<'\n';
    else
        cout<<0<<'\n';
    return 0;
}



```
