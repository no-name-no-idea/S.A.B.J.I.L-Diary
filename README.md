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

6. DB에서 INDEX를 잘 활용하자.(ex. 두개의 키를 묶어서 Primary Key를 만든 후 primary key를 다른 테이블에서 Foreign Key로 사용할 때)  
`NO 삽질 💭 / 2021-03-24`

7. go에서 cgo를 이용하면 C를 사용할 수 있다. 다만 GCC가 설치되어 있어야 C코드가 작동한다. 리눅스 환경에서는 GCC를 쉽게 설치할 수 있지만 윈도우 환경에서는 `mingw-w64`를 이용하여 GCC를 설치한뒤 환경변수를 등록해줘야 작동을 한기 때문에 복잡하다.   
`대략 1시간 삽질 🕐 / 2021-03-24`

8. postman을 이용하여 서버 api를 테스트 할 땐 request에서 어떤 형식을 보내고 있는지 확인하자.😂  
gin에서 post를 통해 request로 들어온 body 값을 볼려고 POST 요청시 계속 오류가 나서 request 처리를 방법을 다 시도해봤다. 하지만 계속 오류가 나서 요청을 보낸 Postman을 확인해보니 슬프게도 JSON이 아닌 Text형태로 보내고 있었다.🤣🤣🤣  
`3시간 삽질 🕐 / 2021-03-25`

9. 문자열과 변수를 합칠 땐 변수의 타입을 확인하자. 만약 변수가 int라면 string으로 꼭 감싸주자  
`5분 삽질 5️⃣ / 2021-03-25`

10. PostgreSQL에서 자동 순번 증가를 위해 IDENTITY (1, 1) 구문을 사용하면 밑의 오류가 뜰 것이다.  
`ERROR:  syntax error at or near "IDENTITY"`  
PostgresSQL에서는 위의 구문 대신 GENERATED { ALWAYS | BY DEFAULT } AS IDENTITY 를 지원한다.  
`30분 삽질 🕧 / 2021-03-25`  

11. 쿼리문 오타에 조심하자 쿼리문중 PROJECT가 PORJECT로 오타가 났는데 다른 오류인줄 알고 삽질을 했다.  
`1시간 삽질 🕐 / 2021-03-29`  

12. gRPC의 protoc 명령어를 이용해 .proto 파일을 컴파일 하려고 하는데 `--go_out: protoc-gen-go: Plugin failed with status code 1.` 오류가 떴다.  
문제 원인은 protocbuf에는 go 컴파일이 기본 지원이 되지 않는다. 그래서 `go get -d -u github.com/golang/protobuf/protoc-gen-go`을 통하여 go 컴파일러를 따로 집어 넣어줘야 하였다. 하지만 저 명령어로 get을 했다해서 끝난것이 아니라 gopath로 지정한 폴더의 bin에 가면 protoc-gen-go.exe 파일을 설치한 protocbuf의 bin으로 이동시킨 후 protocbuf의 bin 폴더를 환경변수 설정을 시켜주어야 한다.  
`4시간 삽질 🕓 / 2021-03-31`  

13. gRPC의 서버쪽 코드를 작성하다보면 `RegisterAddServiceServer(s *grpc.Server, srv AddServiceServer)`에서 구조체를 사용하여 서버를 띄어줘야 한다. 이 때 .proto에 선언한 함수들에 대하여 서버에서 모두 함수 작성을 하지 않으면 오류가 발생하게 된다.   
`cannot use (server literal) (value of type server) as proto.AddServiceServer value in argument to pb.RegisterAddServiceServer: missing method ConnectServer`  
때문에 테스트를 하더라도 모든 함수를 조금이라도 작성한 후에 해야 오류없이 진행할 수 있다.  
`5분 삽질 5️⃣ / 2021-04-05`  

14. query문의 문법은 언제나 다시 확인해 보아야한다. `insert into () value ()` => `insert into () values ()`  
`5분 삽질 5️⃣ / 2021-04-07`

15. gin에서 http 코드 반환시 존재하지 않는 코드를 반환하면 에러가 난다. `ex) 1번 코드 반환`  
`5분 삽질 5️⃣ / 2021-04-08`

16. go 테이블을 전체 조회할 일이 있으면 그 테이블의 default 값을 설정을 해두는 편이 좋다. 만약 아무런 값이 안들어 있으면 조회한 값을 Scan()하려 할때 에러가 발생한다.  
`10분 삽질 🔟 / 2021-04-09`

17. sql에서 where 조건으로 boolean type을 이용한다면 `where boolean == true` 가 아니라 `where boolean`을 사용한다.  
`5분 삽질 5️⃣ / 2021-04-09`
