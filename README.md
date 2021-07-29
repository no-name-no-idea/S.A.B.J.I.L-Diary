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

18. 서버에서 에러 처리를 할 때 http code 뿐만 아니라 따로 message를 다르게 작성하면 에러 발생 위치를 찾기 편하다.   
`NO 삽질 💭 / 2021-04-12`  

19. 밑에 코드에서 `defer rows.Close()`에서 `defer`을 빼고 써서 for문이 동작이 안됬다.  
`30분 삽질 🕧 / 2021-04-13`  
```go
	selectStmt := `select * from table`
	rows, err := db.Query(selectStmt)
	if err != nil {
		c.JSON(http.StatusInternalServerError, gin.H{"error": err.Error(), "message": "Failed to select"})
		return
	}

	defer rows.Close()

	for rows.Next() {

		err = rows.Scan(&Id, &Name)
		if err != nil {
			c.JSON(http.StatusInternalServerError, gin.H{"error": err.Error(), "message": "잘못된 형식"})
			return
		}

	}
```

20. 언제나 오타 조심 vue-bootstrap을 사용하여 vue 작성 중 `:items` 를 `:item` 으로 작성함.... 이런 오타는 에러로도 표시가 안된다.
`5분 삽질 5️⃣ / 2021-04-14`  

21. vue를 이용하여 웹에 table을 그릴 때 데이터를 많이 가지고 있으면 웹이 느려지는 줄 알고 db에서 사용할 때마다 불러올 생각을 하였었다. 하지만 데이터를 가지고 있는 것과 별개로 그 많은 데이터들을 화면에 표시하여서 웹이 느려지는 것이 컸다. 실제로 데이터를 가지고 있고 화면에는 일부 데이터만 표시를 하였는데 느려짐이 발생하진 않았다.  
`NO 삽질 💭 / 2021-04-15`  

22. `Elements in iteration expect to have 'v-bind:key' directives  vue/require-v-for-key`  
v-for 사용시 `v-bind:key=""`를 사용하여 key값을 정해주지 않으면 위에 오류가 난다.  
`5분 삽질 5️⃣ / 2021-04-16`   

23. `Avoid using non-primitive value as key, use string/number value instead.`   
v-for 사용시 위의 warning 메시지가 뜬다면 v-bind:key를 숫자나 문자열이 아닌 다른 형식(json, array)를 사용하고 있는 것이다.  
`5분 삽질 5️⃣ / 2021-04-16`   

24. 대용량 데이터를 처리할 때에는 되도록 map과 append()(또는 동적 할당)을 사용하지 않는 것이 좋다. 많은 메모리량을 가지지 않는 이상 프로그램 동작이 느려지기 때문이다.
`NO 삽질 💭 / 2021-04-16`  

25. Query()에서 결과값이 1개일때는 Query()보다 QueryRow().Scan()을 이용하는 것이 좋다
`NO 삽질 💭 / 2021-04-20` 

26. golang `_test.go`를 통해 테스트를 할 때 Test 함수는 함수명에 꼭 Test가 먼저 오게 만들어야 한다.  
go test를 하였을 때 `testing: warning: no tests to run`가 뜬다면 꼭 한번 확인해 보아야 한다.  
`5분 삽질 5️⃣ / 2021-04-21` 
~~~go
// 올바른 함수명
func TestCode(t *testing.T) {
	...
}

// 잘못된 함수명
func CodeTest(t *testing.T) {
	...
}
~~~  

26. 패키지에 있는 전역 변수를 가져다 쓰고 싶을 때는 첫글자를 대문자로 해주어야 public으로 선언해서 가져다 쓸 수 있다.  
이걸 몰라서 일주일 동안 패키지 분리를 못하고 있었다.  
`1주 삽질 1️⃣ / 2021-04-21` 

27. go에서 의존성 관리는 기본적으로 go mod를 지원하고 있다. (의존성 관리 도구 찾다가 알음;;)  
`NO 삽질 💭 / 2021-04-22`  

28. go에서 문자열을 합칠 때 속도는 Buffer.WriteString() -> Join() -> +연산자 -> fmt.Sprintf() 이다.  
사실상 fmt.Sprintf()를 제외한 나머지의 속도 차이는 미미하면 갯수에 따라 바뀔수도 있다.  
`NO 삽질 💭 / 2021-04-26`  

29. 숫자를 문자열로 변활 할 때 fmt.Sprintf()를 사용하기보다. strconv 패키지를 활용하는 것이 좋은 퍼포먼스를 낼 수 있다.  
`NO 삽질 💭 / 2021-04-26`  

30. error 핸들링에 panic() 사용을 지양해야 한다.  
`NO 삽질 💭 / 2021-04-27`  

31. vue에서 v-bind를 이용하여 img 주소를 남길때 현 vue 프로젝트의 이미지를 나타내고 싶다면 require()을 사용하여야 이미지를 포함하여 보여준다   
`NO 삽질 💭 / 2021-05-03`

32. css작성할 때 세미콜론(;)을 작성안하는걸 조심하자. 세미콜론 하나 빠졌다고 다른화면이 되있더라... 빨리 scss를 도입해야겠다.  
`5분 삽질 5️⃣ / 2021-05-04`

33. vue에서 상위 컴포넌트에서 하위 컴포넌트로 데이터 전달을 v-bind, props를 이용하여,  
반대로 하위 컴포넌트에서 상위 컴포넌트로 데이터 전달은 v-on, $emit을 이용하여 전달이 가능하다.  
`NO 삽질 💭 / 2021-05-10`

34. rest api에서 무엇으로 요청했는지 확인하자.  
`2분 삽질 2️⃣ / 2021-05-18`

35. gorm을 이용하면 귀찮은 쿼리문을 직접 작성할 필요가 없다. 단, 테이블 이름을 복수형으로 선언하여야 gorm이 인식을 한다.(예: user -> users)  
단복수 차이가 없는 단어의 경우 또한 고려해야 한다. (예 : equipment의 경우는 단복수가 차이가 없기 때문에 그대로 사용해야한다.)  
`NO 삽질 💭 / 2021-05-18`

36. git commit시 하위 디렉토리에 .git이 있을 경우 서브모듈로 인식한다.  
그래서 .git을 제거 하지 않고 push시 해당 디렉토리를 확인하기 어렵다.  
혹여나 push를 했다면 reset을 하고 다시 push하기를..  
`NO 삽질 💭 / 2021-05-24`

37. go에서 여러 go루틴을 실행할 때 공유 자원 때문에 mutex를 사용하였다. 공유 자원으로 bool 객체를 하나 생성하여 go루틴을 내의 for문을 빠져나오도록 설계를 하였는데. 다음과 같은 실수를 하였다.  
~~~go
		s.rwMutex.RLock()
		if s.done {
			break
		}
		s.rwMutex.RUnlock()
~~~  
s.done을 확인한 후 break를 하는데 문제는 break가 작동되면 s.rwMutex.RUnlock()이 작동하지 않게 된다.  
이 문제로 다시 go 루틴을 실행할 때 s.done을 다시 false로 만들고 시작하는데 mutex unlock이 되지 않아. 멈춰버리는 현상이 발생하였다.  
`2시간 삽질🕑 / 2021-05-26`  
  
38. gorm에서 Where() + Find() + Join()은 작동되지 않는다. Where과 Join을 같이 사용하고 싶다면 Table() + Where() + Join() + Scan()을 사용하여야 한다.  
`30분 삽질 🕧 / 2021-05-28` 

39. gorm은 struct의 맴버 이름을 가지고 컬럼을 구분한다.  
ex) enabled라는 컬럼을 조회할 때 만약 struct 맴버 내의 이름이 enable로 되어있으면 제대로된 값을 가져오지 못한다.  
`30분 삽질 🕧 / 2021-05-28` 

40. delete로 요청을 보낼 시 body가 거절 당할 수 있다. 되도록 query 내에서 처리하도록 해야겠다.  
`1시간 삽질 🕐 / 2021-05-31` 

41. 변수명을 헷갈리게 지으면 에러 찾기가 힘들다. 같은 이름의 앞자리 대소문자만 다르게 변수명을 만들지 말자.  
`30분 삽질 🕧 / 2021-06-01` 

42. .vue 작성시 공통되는 css부분은 분리해내자. style="" 형식으로 처음쓰면 나중에 다시 리팩토링하는 과정이 필요하다(특히 반응형 제작시).  
`30분 삽질 🕧 / 2021-06-14` 

43. css에서 `position: absolute;`를 사용할 땐 길이를 %단위로 주면 안된다. 화면 사이즈가 바뀔 때마다 위치가 바뀌는걸 볼 수 있다.  
`10분 삽질 🔟 / 2021-06-15`  

44. 회사 사내망 전용으로 열어둔 gitlab ce 서버의 외부에서 접속을 한 흔적을 발견하였다. admin 계정으로 접속했는데 처음보는 유저가 생성되어 있었다. 확인해 보니 회사 고정 ip를 통해 gitlab을 접속할 수 있었고 원인은 공유기의 dmz설정이 되어있어서 고정 ip로 요청을 하면 서버컴으로 요청을 보내는 상황이 발생하였다. dmz설정을 없애고 gitlab의 log 파일을 확인하여 정보가 유출 된 것이 있는지 확인을 하였다. 다행히 빠져나간 정보는 없었고 localhost에서만 접속할 것이여서 빼놓았던 메일 확인을 다시 넣어 두었다.    
`4시간 삽질🕓 / 2021-06-22`  

45. ~~gin + vue 에서 다른 라우터로 변경할 땐 src="" 말고 to="" 사용을 추천한다.~~  
`1시간 삽질🕐 / 2021-06-23`  

46. gin에서 BindJSON은 한 번 밖에 실행이 안된다. 만약 유동적으로 req를 처리해야할 땐 map[string]insterface{} 자료형의 변수에 BindJSON을 해주자.  
`1시간 삽질🕐 / 2021-06-24`  

47. go 개발 시 windows에서 daemon 사용법에 대해 검색시 키워드를 `daemon`보다는 `service`로 검색하는 것이 더 좋다. (linux는 daemon, window는 service)  
`2시간 삽질🕐 / 2021-07-12`  

48. chrome remote desktop 설치시 .msi 파일이 없다고 에러가 뜰때에는 https://dl.google.com/dl/edgedl/chrome-remote-desktop/chromeremotedesktophost-{해당버전}.msi 에 접속하여 다운로드를 받아 설치하면 된다.  
`30분 삽질 🕧 / 2021-07-14`  

49. go 1.5버전 이후로 cross compile을 지원한다. 괜한 삽질(리눅스 pc에 go를 설치 후 빌드를 하는 행위 등) 말고 `set GOOS=linux`를 이용하자. (ps 환경말고 cmd 창에서 실행하는걸 추천한다)  
`기타🎸 / 2021-07-19`  

50. 세상의 모든 답까진 아니더라도 왠만한 답은 튜토리얼안에 있다. 공식문서를 꼭 챙겨보자   
`기타🎸 / 2021-07-28`  

51. c#에서 grpc를 사용할 때에는 proto 파일에 `option csharp_namespace = "<NAME>";`을 넣은 뒤 .cs파일에 namespace와 맞춰주면 된다.   
`1시간 삽질🕐 / 2021-07-29`  

51. c#에서 grpc를 사용할 때 .proto에서 repeated 생성하면 readonly 상태이다. 때문에 여러 삽질을 거쳐야 사용할 수 있다.   
https://stackoverflow.com/questions/16617933/protobuf-net-generated-class-from-proto-is-repeated-field-supposed-to-be-re 참조  
`1시간 삽질🕐 / 2021-07-29`  
