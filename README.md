# S.A.B.J.I.L-Diary

1. go에서 PostgreSQL 쿼리문 작성시 “”(큰따옴표/Double quotes)는 대소문자 구분시 사용  ‘’(작은따옴표/Single quote)는 문자열이다. 만약 지키지 않을 시 `panic: pq: column "" does not exist` 를 보게 될 것이다.  
`약 1시간 반 삽질 🕜 / 2021-03-18`

2. go에서 "encoding/json"를 사용해 struct을 JSON 형식으로 변환할 때 struct안의 멤버 이름 첫글자를 대문자를 사용하지 않으면 변환이 안된다.   
`1시간 반 삽질 🕜 / 2021-03-19`
