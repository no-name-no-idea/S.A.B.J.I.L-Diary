# S.A.B.J.I.L-Diary ⛏

1. go에서 PostgreSQL 쿼리문 작성시 “”(큰따옴표/Double quotes)는 대소문자 구분시 사용  ‘’(작은따옴표/Single quote)는 문자열이다.  
만약 지키지 않을 시 `panic: pq: column "" does not exist` 를 보게 될 것이다.  
`약 1시간 반 삽질 🕜 / 2021-03-18`

2. go에서 "encoding/json"를 사용해 struct을 JSON 형식으로 변환할 때 struct안의 멤버 이름 첫글자를 대문자를 사용하지 않으면 변환이 안된다.   
`1시간 반 삽질 🕜 / 2021-03-19`

3. package는 전역으로 선언한 것들(변수, 함수, 구조체)을 같은 package안에서 불러 쓸 수 있다. 만약 공용으로 사용될 것들이 있다면 한 파일로 만들어 두면 편할 것 같다.  
`NO 삽질 💭 / 2021-03-22`

4. PostgreSQL를 조회할 때 오류가 뜬다면 내가 Table Create 할 때 접속한 DB를 다시 한번 확인해 보는 것도 답이다.(다른 DB에 Table을 만들어 놓고서 나중에 알음😅)  
`30분 삽질 🕧 / 2021-03-22`

5. go에서 구조체 배열을 동적으로 할당하고 싶을 땐 make([]array,0)로 배열 길이를 0으로 할당해준 뒤 append(array, struct)를 통하여 할당을 할 수 있다.   
`1시간 삽질 🕐 / 2021-03-23`
