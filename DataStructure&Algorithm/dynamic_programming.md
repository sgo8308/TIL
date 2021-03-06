### 다이내믹 프로그래밍의 문제 풀이 접근 방식
    1. 문제를 보고 DP 문제일지 파악한다. 
        - 문제가 더 작은 문제로 쪼개질 수 있고 그 문제들의 답이 여러번 활용될 수 있다면 DP문제일 가능성이 크다.
        - 최대, 최소, 모든 방법의 수, 어떤 방법이 가능한지 등등의 문제는 DP문제일 가능성이 크다.
    2. 그리디 방식과 겹치는 경우가 많으므로 그리디 방식으로 먼저 시도해본다.
        
        시도해보고 반례를 생각하여 그리디로 풀 수 없다는 확신을 얻으면 다음으로 넘어간다.
        
    3. 점화식을 세운다.
        
        작은 문제부터 본 문제까지 모든 시나리오를 설명할 수 있는 점화식을 세운다.
        
        이 때 점화식은 작은 문제의 해답을 이용하는 방식이어야 한다.
        
    4. 구현한다.