# 포드 풀커슨 알고리즘 (Ford-Fulkerson)

- 최초의 네트워크 유량 알고리즘
- 네트워크 플로우 알고리즘의 기본적인 알고리즘    


[네트워크 플로우]  
그래프의 경로의 길이가 아닌 '용량'의 관점에서 바라보는 시점  

## 단어 정리
---

용량 (capacity) : 두 정점 사이에 최대로 흐를 수 있는 양 = 간선에서 소화 가능한 최대 양  
유량 (flow) : 두 정점 사이에 흐르는 양 = 간선에서 사용하고 있는 양  
소스 (source) : 유량이 시작되는 정점  
싱크 (sink) : 유량이 도착하는 정점  
**증가경로 (augmenting path) : 소스에서 싱크로 유량을 보내는 경로**

---

## 알고리즘 작동 순서
1. 소스에서 싱크로 가는 경로(=증가경로) 찾기  
    !! 이때 해당 경로는 반드시 여유 용량이 남아있어야 함 !!  
2. DFS를 이용해 증가경로를 찾고 찾은 만큼 유량을 흘려보내기  
3. 더 이상 증가경로를 찾을 수 없을 때까지 1, 2번을 반복하기  

[DFS 깊이 우선 탐색]  
루트 노드에서 시작해서 다음 분기로 넘어가기전에 해당 분기를 완벽하게 탐색하는 방법  

## 알고리즘 설명

위의 알고리즘 작동 순서에 맞춰 S에서 T로 가는 최대 유량을 구한다. (=등가경로를 찾는다.)

![](https://postfiles.pstatic.net/MjAyMjA0MjhfODgg/MDAxNjUxMTQ0MTgxMjY3.nNw0Hu7w-_0yKdoBJ4ljWhh0v4N544LahxhWx5kC3zQg._iXq1IJPVihFAnleS4D0b41zDI-_SjGVV9gWcP_ONP8g.PNG.kimsanga0430/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C1.PNG?type=w773)


DFS를 사용    
S -> A = 3     
A -> D = 3   
D -> T = 3  
경로에서 보낼 수 있는 최대 유량은 각각의 구간에 남은 용량의 최소값  
S -> A -> D -> T 경로에서 찾은 3을 흘려보냄.  
Total : 3  

![](https://postfiles.pstatic.net/MjAyMjA0MjhfMTM3/MDAxNjUxMTQ0MTgxMjcy.YAqvSThlIR32MOvKbyOuppT-njp0ttIZSKvUqcOdsUEg.t3l2a2o2O3jr0CIyDSd6UAiw3fFGCMOGCTS-BfgvmMcg.PNG.kimsanga0430/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C2.PNG?type=w773)

S -> B = 2  
B -> E = 2  
E -> T = 2  
S -> B -> E -> T 경로에서 찾은 2를 흘려보냄.  
Total : 5

![](https://postfiles.pstatic.net/MjAyMjA0MjhfNDgg/MDAxNjUxMTQ0MTgxMjY3.gqGXdOJ8ceaxt3-pqhJezHIfpAscYAnGEvgxx-_Vz6og.dtp7MeYaLtIw3Iy95hAoLY-Y82WtbjSLfJhFt9X1CDkg.PNG.kimsanga0430/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C3.PNG?type=w773)  

S -> B = 1  
B -> E = 1  
E -> T = 1  
S0> B -> E -> T 경로에서 1을 흘려보냄.
Total : 6  

![](https://postfiles.pstatic.net/MjAyMjA0MjhfODAg/MDAxNjUxMTQ0MTgxMjcx.pIyZ63yiXoZ25YjnFLMGVGJkHEDH--p1xxWLMeifm5Ig.FnvRxOFDln1zqCfrSGOHxEWDMxU-2288C1Ic0hm4lhkg.PNG.kimsanga0430/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C4.PNG?type=w773)

S -> C = 5  
C -> F = 5  
F -> T = 5  
S -> C -> F -> T 경로에서 5를 흘려보냄.  
Total : 11

![](https://postfiles.pstatic.net/MjAyMjA0MjhfMjYw/MDAxNjUxMTQ0MTgxMjcy.q0-2kyerc7FiRrJBqWlc_OkSLWfMYQWhO2hXHrUV8Q0g.lWxm80_VN6cPdOPIspJQEy6A6CBadxv5ZuD0-CKg0OUg.PNG.kimsanga0430/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C5.PNG?type=w773)

S -> A -> D -> T = 3  
S -> B -> D -> T = 5  
S -> B -> E -> T = 6  
S -> C -> F -> T = 11  
![](https://postfiles.pstatic.net/MjAyMjA0MjhfMjM4/MDAxNjUxMTQ0MTgxMjcy.xxHcUJdVdzMjfeIih2qDjhbQBk_XtpFCLyoUcqy782cg.Fs2AGWZPUZtWJ5gEs4lYTipcU-x0spq34Yg1IGOYz7sg.PNG.kimsanga0430/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C6.PNG?type=w773)

[유량의 흐름을 알 수 있는 방법]  
역간선이 있는 상태에서, 알고리즘 작동 순서 1~3을 다시 반복함  
S -> C -> F -> E -> A -> D -> T  

### 내가 구한 유량과 최대 유량이 다를 때 

더 이상 증가경로가 보이지 않을 때, 기존의 간선과 반대 방향인 용량이 0인 간선을 추가함.  
만약 기존의 간선에 유량 n이 흐르고 있었다면, 반대 방향의 간선으로는 유량 -n이 흐른다고 판단함.  
=> 반대 방향의 간선에 n만큼의 여유 용량이 생기므로, 해당 간선에 유량을 흘려줄 수 있음. 

(반대 방향의 간선에 유량이 흐름 = 기존 간선에 있던 유량을 취소하고 우회)  

## 코드 구현
```C
 public static int capacity[][];
    public static int flow[][];
    public static int path[];
    public static boolean visited[];
    public static LinkedList<Integer> graph[];

    public static boolean dfs(int start) {
        if (start == Sink) {
            return true;
        }

        visited[start] = true;
        LinkedList<Integer> nexts = graph[start];
        for (int next: nexts) {
            if ( !visited[next] && capacity[start][next] - flow[start][next] > 0) {
                path[next] = start;

                if (dfs(next)) { // 경로를 끝까지 찾으면 탈출, 아니면, 끝까지 찾기 재시도
                    return true;
                }
            }
        }
        return false;
    }

    public static boolean bfs() {
        Arrays.fill(path, -1);
        Queue<Integer> q = new LinkedList<Integer>();
        q.add(Source);

        while (!q.isEmpty()) {
            int from = q.poll();
            LinkedList<Integer> nexts = graph[from];

            for (int next: nexts) {
                if ( path[next] == -1 && (capacity[from][next] - flow[from][next]) > 0 ) {
                    path[next] = from;
                    q.add(next);

                    if (next == Sink) {
                        break;
                    }
                }
            }
        }

        if (path[Sink] == -1) {
            return false;
        }

        return true;
    }

    // O(VE^2)
    public static int EdmondsKarp() {
        int total = 0;
        while (bfs()) {
            // flow값 찾기
            int flowNum = Integer.MAX_VALUE;
            for(int i = Sink; i != Source; i = path[i]) {
                int from = path[i];
                int to = i;
                flowNum = Math.min(flowNum, (capacity[from][to]) - flow[from][to]);
            }

            // flow흘려 보내기, 역방향도 반드시!!!!
            for(int i = Sink; i != Source; i = path[i]) {
                int from = path[i];
                int to = i;

                flow[from][to] += flowNum;
                flow[to][from] -= flowNum;
            }

            total += flowNum;
        }
        return total;
    }

    // O((V+E)F)
    public static int FordFulkerson() {
        int total = 0;
        while (dfs(Source)) { // dfs로 경로 찾기(증가경로), 경로가 더이상 없으면 종료임.
            // 찾은 경로에서 차단 간선 찾기 min (capacity[u][v] - flow[u][v])
            // 결국 의미는 경로에서 흘릴수 있는 최대의 유량(flow)을 찾기
            int flowNum = Integer.MAX_VALUE;
            for(int i = Sink; i != Source; i = path[i]) {
                int from = path[i];
                int to = i;
                flowNum = Math.min(flowNum, (capacity[from][to]) - flow[from][to]);
            }
            // 찾은 경로에 유량을 흘려보내기, 역방향도 반드시!!!!
            for(int i = Sink; i != Source; i = path[i]) {
                int from = path[i];
                int to = i;

                flow[from][to] += flowNum;
                flow[to][from] -= flowNum;
            }

            total += flowNum;

            // 찾은 경로를 초기화해서 dfs로 경로 찾기를 Source > Sink 까지 다시 할 수 있게 함.
            Arrays.fill(path, -1);
            Arrays.fill(visited, false);
        }
        return total;
    }
    ```

## 성능 분석

시간복잡도 = O((V + E)F) = O(EF)  
