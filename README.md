# Ford-Fulkerson Algorithm
포드풀커슨 알고리즘은 최초의 네트워크 유량 알고리즘 으로, **특정한 지점에서 다른 지점으로 데이터가 얼마나 많이 흐르고 있는 지**를 측정하는 알고리즘 입니다. 교통 체증이나 네트워크 데이터 전송 등 다양한 분야에 활용이 되고 있습니다.  

# 쓰이는 용어  

`용량` 두 지점 사이에서 흐를 수 있는 최대의 양입니다.  
`유량` 두 지점 사이에서 흐르는 양입니다.  
`소스` 유량이 시작되는 정점입니다. 보통 S로 많이 나타냅니다.  
`싱크` 유량이 도착하는 정점입니다. 보통 T로 많이 나타냅니다.  
`증가경로` *소스*에서 *싱크*로 유량을 보내는 경로를 나타냅니다.  


# 동작 방식  

네트워크의 모든 간선의 유량을 0으로 시작하고, *소스*에서 *싱크*로 보낼 수 있는 경로로 유량을 반복해서 보내면 됩니다.  
이 때 BFS(너비 우선 탐색)을 이용하는 것이 일반적입니다.  

!
