# Ford-Fulkerson Algorithm
포드풀커슨 알고리즘은 최초의 네트워크 유량 알고리즘 으로, **특정한 지점에서 다른 지점으로 데이터가 얼마나 많이 흐르고 있는 지**를 측정하는 알고리즘 입니다. 교통 체증이나 네트워크 데이터 전송 등 다양한 분야에 활용이 되고 있습니다.  

# 쓰이는 용어  

`용량(Capacity)` 두 지점 사이에서 흐를 수 있는 최대의 양입니다. **ex) c(u, v): 정점 u에서 v로 전송할 수 있는 최대 용량**  
`유량(Flow)` 두 지점 사이에서 흐르는 양입니다. **ex) f(u, v): 정점 u 에서 v 로 실제 흐르고 있는 유량**  
`잔여 용량 (Residual Capacity)` r(u, v) = c(u, v) – f(u, v)  
`소스(Source)` 유량이 시작되는 정점입니다. 보통 S로 많이 나타냅니다.  
`싱크(Sink)` 유량이 도착하는 정점입니다. 보통 T로 많이 나타냅니다.  
`증가경로` *소스*에서 *싱크*로 유량을 보내는 경로를 나타냅니다.  


# 동작 방식  

* 각 간선에 정해진 용량이 있을 때, 임의의 A에서 B로 최대로 보낼 수 있는 유량의 크기를 구하는 문제입니다.  
* 네트워크의 모든 간선의 유량을 0으로 시작하고, *소스*에서 *싱크*로 보낼 수 있는 경로로 유량을 반복해서 보내면 됩니다.  
이 때 DFS을 이용하는 것이 일반적입니다.  

![ex1](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTfSO1%2Fbtq52A4jkfN%2FGjzL4h2tioTZPleBBk2rk1%2Fimg.png)  
먼저 모든 경우의 수를 찾기 위해서 **유량을 모두 0으로 설정**합니다.  

![ex2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FC9q5W%2Fbtq53kNjeVm%2FbbUemxytIsc3fkTNn1AUV1%2Fimg.png)  
해당 그래프의 최대 유량의 경로는 위와 같습니다.  
만약 s->a->b->t에 대한 경로가 먼저 찾아졌다면 s->b, a->t간선으로는 유량을 보낼 수 없습니다.  
따라서 최대 유량이 1인 상태에서 프로그램은 중지하게 됩니다.
여기서 최대 유량 알고리즘은 모든 가능한 경로를 다 계산해주기 위해서 음의 유량도 계산해줍니다.   

![ex3](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbnif4y%2Fbtq54pt0vZg%2FuD2qgmasWB4l91LMdHckfk%2Fimg.png)  
위 그림과 같이 알고리즘에서 **음의 유량이 존재한다고 가정**을 해서 가능한 모든 경로를 더 추가적으로 탐색하게 합니다.  
a->b로 1만큼 흐르고 있지만 b->a로 -1만큼 흐르고 있다고 가정을 합니다.  
실제로는 용량이 존재하지 않기 때문에 용량은 0이 됩니다.  
-1 < 0이기 때문에 계산적으로는 가능하다고 할 수 있습니다.  
따라서 간선 b → a의 잔여 용량 r(b, a)은 **c(b,a) - f(b, a) = 0 - ( - 1 ) = 1** 이 됩니다.  
즉, b → a로 1의 유량을 추가적으로 흘려보낼 수 있게 됩니다.
결과적으로 모든 경우의 수를 음의 유량을 고려해서 찾을 수 있습니다.  

# 포드풀커슨 알고리즘 성능 분석  

포드풀커슨 알고리즘은 DFS 방식으로 증가 경로를 찾습니다.  
*애드몬드-카프 알고리즘* 이라는 알고리즘은 BFS 방식으로 증가 경로를 찾습니다.  
포드풀커슨의 시간복잡도는 O((|E|+|V|) * F) 이고, 애드몬드-카프의 시간복잡도는 O(|V| * (|E|^2)) 이므로  
F, 즉 최대 유량이 클 경우에는 포드풀커슨 알고리즘이 애드온드-카프 알고리즘보다 비휴율적일 수 있습니다.  
하지만 문제의 Flow(최대 유량)가 적고, Edge(간선)가 많으면 오히려 포드-풀커슨 알고리즘이 효율적일 수 있습니다.  
