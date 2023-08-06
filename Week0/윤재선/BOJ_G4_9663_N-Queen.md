# BOJ_G4_9663_N-Queen[2023.08.06] </br>

## 알고리즘 종류
```
브루트포스 알고리즘
백트래킹
```

## 해설 및 느낀점
```
바킹독님 유튜브에서 힌트를 조금 얻어서 풀었다. 좀 어려웠는데 dfs와 살짝 다르게 visited 배열을 int형으로 선언하고 상태공간트리에서 올라갈 때
visited에 1을 더해줬던걸 빼는 연산을 통해 문제를 풀었다. 각 행에 queen이 한개만 올 수 있다는 사실이 중요했다. 이걸로 왼쪽 오른쪽은 visited 연산을 안해도 됬다.
못풀줄 알았는데 풀어서 신기하다
```
## 코드
```c++
#include <bits/stdc++.h>
#define MAXNUM 15
#define DIR 6
using namespace std;
int arr[MAXNUM][MAXNUM];
int visited[MAXNUM][MAXNUM];
int n;
int ans=0;

int dy[DIR]={1,0,1,-1,-1,1};
int dx[DIR]={0,-1,1,1,-1,-1};
bool inRange(int y, int x)
{
    return (y<n && y>=0 && x<n && x>=0);
}
void put(int y,int x)
{
    visited[y][x]++;
    for(int i=0;i<DIR;i++)
    {
        int new_y=y+dy[i];
        int new_x=x+dx[i];
        while(inRange(new_y,new_x))
        {
            visited[new_y][new_x]++;
            new_y=new_y+dy[i];
            new_x=new_x+dx[i];
        }
    }
}
void retreive(int y,int x)
{
    visited[y][x]--;
    for(int i=0;i<DIR;i++)
    {
        int new_y=y+dy[i];
        int new_x=x+dx[i];
        while(inRange(new_y,new_x))
        {
            visited[new_y][new_x]--;
            new_y=new_y+dy[i];
            new_x=new_x+dx[i];
        }
    }
}
void func(int col)
{
    if(col==n)
    {
        ans++;
        return;
    }
    for(int i=0;i<n;i++)
    {
        if(!visited[col][i])
        {
            put(col,i);
            func(col+1);
            retreive(col, i);
        }
    }
    return;
}
int main()
{
    cin>>n;
    func(0);
    cout<<ans<<'\n';
    return 0;
}
```
