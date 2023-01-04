# 저장소 설명
https://gyoogle.dev/blog/interview/
<br/>(해당 저장소에 정리가 너무나 잘 되어 있기 때문에, '위 저장소 내용+alpha' 또는 몇가지를 내가 원하는 표현으로 바꾸어 기록하는 용도의 저장소)


# 운영체제
## 인터럽트
프로그램 실행 중 예기치 못한 상황이 발생한 경우에 실행 중인 프로그램을 중단하고, 해당 상황에 대한 처리가 우선적으로 필요함을 CPU에게 알리는 것을 의미.
인터럽트는 크게 3가지로 구분되는데, 내부 인터럽트는 오버플로우 등 잘못된 명령 또는 데이터를 사용할 경우 발생하고, 외부 인터럽트는 입출력 장치나 전원 등의 외부적인 요인, 소트프웨어 인터럽트는 특정 프로그램 처리 중에 별도 요청에 따라 발생한 인터럽트이다.
내, 외부 인터럽트는 CPU의 하드웨어 신호에 의해 발생하는 인터럽트이며, 소프트웨어 인터럽트는 명령어 수행에 의해 발생.
### 처리 순서
1. 인터럽트 요청 신호
2. 프로그램 실행 중단
3. 현재 실행 중인 프로그램 복귀 주소를 Stack에 저장
4. 문제 파악 등 인터럽트 처리 루틴을 실행
5. 문제 해결을 위한 인터럽트 서비스 루틴 실행
6. 상태 복구가 중단된 프로그램 재실행
### 우선순위
1. 전원 이상
2. 기계 이상
3. 외부 신호
4. 입/출력
5. 프로그램 검사
6. SVC(SuperVisor Call)

## 스케줄링
언제 어떤 프로세스에 CPU를 할당하는지 결정하는 작업을 CPU 스케줄링이라 하며, 종류로는 크게 선점/비선점 스케줄링이 존재한다.
### 비선점 스케줄링
프로세스가 CPU 점유 시 이를 뺏을 수 없는 방식
FCFS(First Come First Served) : 큐에 도착한 순서로 CPU를 할당
SJF(Shortest Job First) : 수행시간이 가장 짧다고 판단되는 작업을 먼저 실행
HRN(Hightest Response-ratio Next) : 우선순위( (대기시간+실행시간) / 실행시간 )를 계산하여 우선순위가 높은 작업을 먼저 실행

### 선점 스케줄링
프로세스가 실행 중이더라도 운영체제가 강제로 뺏을 수 있는 방식
우선순위 스케줄링(Priority Sheduling) : 우선 순위를 동적, 정적으로 부여해 순위가 높은 순서대로 처리하는 스케줄링으로, 기아(Starvation)라고 하는 우선 순위가 낮은 프로세스를 무한정으로 기다리는 경우가 발생할 수 있다.
RR(Round Robin) : CPU 할당 시간을 각 프로세스에 동일하게 부여하여 정해진 시간만큼만 작업 후 넘어가는 방법
멀티레벨 큐(MultiLevel Queue) : 어떤 프로세스이냐에 따라, 여러 종류의 그룹으로 나눈 뒤 여러개의 큐에 다양한 알고리즘 적용하는 방법

### Sync, Async 전송의 차이점
- Sync(Synchronous)
미리 정해진 양 만큼의 문자열을 하나로 묶어 한 번에 전송하는 방법이며, 송신한 데이터를 수식받는 측에서 정확한 내용을 수신받기 위해 타이밍을 일치시키는 것을 동기식 전송이라고 한다.
전송 효율이 높다는 장점이 있고, 수신측에서 문자를 조립해 비트를 계산하는 기억 장치가 필요해 가격 증가
Async(Asynchronous)
에디터 내 동기 신호를 포함해 데이터를 전송하는 방식으로, 타이밍을 맞추지 않고 문자 단위로 구분해 전송하는 방식이다.
시작 비트와 정지 비트 사이 간격이 가변적이기 때문에 불규칙적이거나 짧은 데이터 전송에 적합하며, 시작 비트와 정지 비트 전송으로 인한 추가적인 오버헤드를 갖는다.

# 네트워크
### DNS RR(Round Robin) 방식
DNS 서버 구성 방식 중 하나로, 도메인에 대한 IP 요청 쿼리를 보내면 Round Robin 방식으로 IP를 반환하는 것이다.
즉, DNS 서버에 대한 Round Robin 형식으로 구성할 경우에는 부하에 대한 걱정이 필요 없기에 로드 벨런서 또한 필요가 없어진다.(자동으로 시간에 따라 스케쥴링이 변화하여)

### 웹 통신 전체적인 흐름(주소창에 URL 입력 시 발생)
1. 사용자가 웹 브라우저를 통해 URL 입력
2. URL의 도메인 네임을 DNS 서버에서 검색하여 IP 찾은 후 URL 정보와 함께 사용자에게 전달
3. 전달받은 내용을 통해 HTTP 요청 메시지 생성하여 TCP로 서버로 전송
4. 서버가 클라이언트의 요청을 받고 응답을 전송
5. 사용자가 홈페이지 이용

# DB
### Key
기본 키는 모든 행 데이터가 고유하게 식별되는 테이블의 해당 열입니다. 테이블의 모든 행에는 기본 키가 있어야하며 두 행은 동일한 기본 키를 가질 수 없습니다. 기본 키 값은 절대로 null이거나 수정하거나 업데이트 할 수 없습니다. 복합 키는 열 세트가 테이블의 모든 행을 고유하게 식별하는 후보 키의 양식입니다.
유니크 키
Unique 키는 유일성을 가지기 위해 설정해 놓은 키로 중복이 되는 것을 방지합니다. Primary 키는 오직 하나만 생성할 수 있지만, Unique키는 여러개 생성이 가능합니다. Primary키의 경우 NULL 값을 허용하지 않지만, Unique 키는 NULL 값을 허용합니다.

### DELETE vs TRUNCATE vs DROP
'DELETE' 연산을 실행 한 후 손실 된 데이터를 검색하기 위해 COMMIT 및 ROLLBACK 문을 수행 할 수 있습니다.
'TRUNCATE' 조작을 실행 한 후 손실 된 데이터를 검색하기 위해 COMMIT 및 ROLLBACK 문을 수행 할 수 없습니다.
'DROP' 명령은 기본 키 / 외래 키와 같은 테이블 또는 키를 삭제하는 데 사용됩니다.

### Join
두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법입니다.
Inner Join 은 2개 이상의 테이블에서 교집합만을 추출
Left Join 은 2개 이상의 테이블에서 from에 해당하는 부분을 추출
Right Join 은 2개 이상의 테이블에서 from과 join하는 테이블에 해당하는 부분을 추출
Outer Join 은 아웃터 조인 또는 풀 조인이라고 말함, 2개 이상의 테이블에서 모든 테이블에 해당하는 부분을 추출

### SQL Injection
SQL injection은 악의적으로 SQL문을 실행해서 비정상적으로 데이터베이스를 조작하는 공격 방법

### Transaction
데이터베이스의 DML(Data Manipulation Language), 즉 삽입(INSERT), 갱신(UPDATE), 삭제(DELETE)와 관련된 논리적인 작업을 말하며, DML 실행과 동시성 제어를 위한 중요한 개념이다.
관계형 데이터베이스 시스템은 데이터를 처리할 때 트랜잭션을 통해 정상 종료나 사용자 프로세스 실패나 시스템 실패와 같은 비정상 종료에 대해 데이터의 신뢰성과 일관성을 보장한다.
즉, 데이터베이스의 데이터 무결성이 보장되는 상태에서 DML 작업을 완수하기 위한 기본 작업 단위이다.
4개 특성 : 원자성, 일관성, 고립성, 지속성
트랜잭션 제어어 : 커밋, 롤백

### Statement vs PreparedStatement
Prepared Statement
쿼리실행 계획 분석과 컴파일이 완료되어서 DBMS의 캐시에 준비되어있는 쿼리를 사용하는 것. 즉 위에서의 4단계 중 parse 과정을 생략하고 나머지 3단계만 실행한다.
장점 : SQL 처리가 빠르며, SQL이 반복적일 때 효과적이다.
단점 : 쿼리 오류 발생 시 분석이 어렵다. 바인드 변수가 일부 위치에서만 사용되기 때문에 동적 쿼리 작성이 어렵다.
Statement
prepared statement와 다르게 4단계를 매번 실행하여 결과 값을 리턴한다.
장점 : 동적 쿼리 실행 가능, 쿼리 실행문 직접 확인 가능
단점 : 반복 실행의 경우 불리, SQLI 공격 가능성

### RDBMS vs NoSQL
RDBMS는 모든 데이터를 2차원 테이블 형태로 표현합니다.
장점 : 스키마에 맞춰 데이터를 관리하기 때문에 데이터의 정합성을 보장할 수 있다.
단점 : 시스템이 커질 수록 쿼리가 복잡해지고 성능이 저하되며 Scale-out이 어렵다(Scale-up만 가능)
NoSQL(Not Only SQL)은 RDBMS와 반대로 데이터간의 관계를 정의하지 않고, 스키마가 없어 좀 더 자유롭게 데이터를 관리할 수 있으며, 컬렉션이라는 형태로 데이터를 관리합니다.
장점 : 스키마 없이 Key-Value 형태로 데이터를 관리해 자유롭게 데이터를 관리할 수 있다.
데이터 분산이 용이하여 성능 향상을 위한 scale-up 뿐만아닌 scale-out 또한 가능하다.
단점 : 데이터 중복이 발생할 수 있고, 중복된 데이터가 변경될 경우 수정을 모든 컬렉션에서 수행해야 한다.
스키마가 존재하지 않기에 명확한 데이터 구조를 보장하지 않아 데이터 구조 결정이 어려울 수 있다.
💡그렇다면 RDBMS와 NoSQL은 어느 경우에 적합한가요?
RDBMS는  또한 중복된 데이터가 없어(데이터 무결성) 변경이 용이하기 때문에 관계를 맺고 있는 데이터가 자주 변경이 이루어지는 시스템에 적합합니다.
데이터 구조가 명확하고, 변경 될 여지가 없으며 스키마가 중요한 경우 사용하는 것이 좋습니다.
NoSQL은  또한 단점에서도 명확하듯 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경될 시 모든 컬렉션에서 수정해야 하기 때문에 Update가 많이 이루어지지 않는 시스템에 좋으며, Scale-out이 가능하다는 장점을 활용해 막대한 데이터를 저장해야 해서 DB를 Scale-out 해야 되는 시스템에 적합합니다.
정확한 데이터 구조를 알 수 없고 데이터가 변경/확장 될 수 있는 경우 사용하는 것이 좋습니다.

### Stored Procedure
데이터베이스에 저장된 SQL명령문을 하나의 함수처럼 실행하기 위한 Query(쿼리)의 집합이다. 같은 쿼리를 반복할 필요가 없어 속도가 빠르고 에러 확률을 감소시킨다.

# Web
### 브라우저 렌더링(작동) 방식
HTTP 모듈 또는 파일 시스템으로 전달 받은 resource stream을 읽는 과정인 1. Loading 과정을 거치고, HTML 마크업을 처리하고 2. DOM Tree를 빌드하며, CSS 마크업을 처리하고 3. CSSOM Tree를 빌드합니다. 생성한 DOM 및 CSSOM 트리를 결합하여 4. 렌더링 트리를 형성하며, 렌더링 트리에서 각 노드의 형태를 계산하여 Box-Model을 생성하는 5. Layout 과정을 거치고, 개별 노드를 화면에 페인트하는 6. Paint 과정을 거쳐 렌더링이 이루어집니다.

### Browser 동작 방식(웹페이지가 사용자에게 보여지는 과정)
웹페이지는 다른 도메인 페이지로 이동하려고 할 때 발생하는 Prompt for unload 과정을 시작으로 Redirect부터 Response 까지의 과정에 해당하는 네트워크 통신 과정을 거칩니다.    
세부적인 과정을 설명하면, 해당하는 URL로 HTTP 요청을 보내는 Redirect, 이미 캐싱된 응답을 확인하여 재사용하는 AppCache 과정을 거치고, DNS를 통해 도메인을 IP주소로 변환한 다음, IP 주소를 통해 TCP 통신으로 서버에 연결하여 Request, Response의 과정을 거칩니다. 응답을 받은 후에는 파일을 파싱하고 렌더링하는 Processing 과정을 거치고 마지막으로 화면에 보여주는 Load 과정을 수행합니다.
(단계마다 꼬리질문이 나올 수 있음)
    
### HTTP Request Method
GET은 동일한 연산을 여러 번 수행하더라도 동일한 결과가 나타나야 한다는 멱등성을 가지고 있고 조회 시에 사용됩니다. POST는 여러 번 수행하더라도 응답은 다를 수 있으며 데이터를 생성/업데이트하기위해 데이터를 전송 시킬 때에 사용됩니다.

### HTTP status Code
1-5의 카테고리에서 특정 상황에 맞는 번호를 "상황"에 매칭 해서 풍부한 응답 결과를 제공할 수 있도록 IANA(Internet Assigned Number Authority로 IP 주소를 관리하는 기관이다)에서 관리하고 있다.
첫 번째 숫자가 카테고리가 되어준다.
1xx (informational response): 정보를 제공하는 응답이다.
2xx (success) : 요청을 성공적으로 받았으며 인식을 했고 수용했다는 것을 의미한다.
3xx (redirection) : 클라이언트의 요청에 대해 "적절한 위치"를 제공하거나 대안의 응답을 제공한다.
4xx (Client Error) : 클라이언트의 잘못된 요청
5xx (Server Error) : 클라이언트의 요청은 정상적이었지만 서버의 문제로 응답이 불가능한 경우. [ 트래픽 관련이 많다. ]   
4xx와 관련된 세부적인 상태 코드들이 매우 중요하다. [ 클라이언트와 관련된 것이기 때문! ]
400 : 클라이언트의 잘못된 문법으로 서버가 이해하지 못한 경우를 의미한다.
401 : 요청을 위한 권한 인증이 필요하다는 상태 코드이다.
403 : 인증은 처리되었으나 해당 자원에 대한 인가를 거치지 않은 경우에 대한 응답이다.
404 : Not Found로 요청한 URI를 찾을 수 없는 경우이다.

### REST API
👉🏻 REST는 Representational State Transfer의 약자입니다. 간단히 말해서 URI와 HTTP 메소드를 이용해 객체화된 서비스에 접근하는 것입니다. REST의 요소로는 크게 리소스, 메소드, 메세지 3가지 요소로 구성됩니다. 예를 들어 "이름이 Tom인 사용자를 생성한다." 라는 호출이 있을 때 "사용자"는 생성되는 리소스, "생성한다."라는 행위는 메소드, 그리고 "이름이 Tom인 사용자"는 메세지가 됩니다. 즉 리소는 http://myweb/users라는 형태의 URI로 표현되며, 메소드는 HTTP Post, 메세지는 JSON 문서를 이용해서 표현됩니다. HTTP에는 여러가지 메소드가 있지만 REST에서는 CRUD에 해당하는 4가지의 메소드 GET, POST, PUT, DELETE를 사용합니다. REST는 리소스 지향 아키텍쳐 스타일이라는 정의에 맞게 모든 것을 명사로 표현하며 각 세부 리소스에는 id를 붙입니다.
    
👉🏻 Restful하게 API를 디자인한다는 것은 URI를 규칙에 맞게 잘 설계했는지의 여부입니다. 규칙의 항목으로는 아래와 같습니다.1. 동일한 URI(End point)의 행위에 맞게 POST, GET, DELETE, PATCH등의 메소드를 사용한다.2. 명사를 사용한다. 리스트를 표현할 때는 복수형을 사용한다.3. URI Path에 불필요한 파라미터를 넣지 않는다. 즉, 단계를 심플하게 설계한다.

### DNS Round Robin
라운드 로빈(Round Robin) 알고리즘은 **서버에 들어오는 요청들을 순서대로 돌아가면서 배정하는 알고리즘**입니다. 뭐가되었든 하나씩 배정하기 때문에 여러 대의 서버 성능이 비슷하고 세션이 오래 지속되지 않는 경우에 적합합니다.    
반면, 최소 연결 방식(Least Connection Method) 은 요청이 서버에 들어왔을 때 **가장 연결이 적은 서버에 배정하는 알고리즘**입니다. 서버 트래픽이 일정하지 않고 세션이 길어질 때 적합합니다.    
이 외에도 서버마다 가중치를 매겨 가중치에 맞게 요청을 배정하는 **가중 라운드 로빈** **방식**, 클라이언트의 IP주소를 해싱하여 분배하는 **IP 해싱 방식**, 서버의 현재 연결 상태와 응답 시간을 고려하여 배분하는 **최소 리스폰 타임** 알고리즘이 있습니다.

### 쿠키 & 세션
먼저 쿠키는 일정시간 임시 데이터를 **클라이언트**인 브라우저에 저장하기 위하여 사용됩니다.
쿠키는 인터넷 쇼핑몰에서 로그인을 하지 않았는데 장바구니 담기가 가능하게 하는데 활용되며, 광고 팝업에 나오는 다시보지않기를 누르면 다음에는 팝업이 나오지 않는 것에도 활용됩니다. 물론 서버 작업을 통해 구현해도 되지만 굳이 저장할 필요가 없다면 서버의 리소스는 아끼는 것이 좋습니다. 또, 매번 서버에서 데이터를 불러오기보단 간단한 값들은 쿠키를 활용하여 저장하면 비용을 아낄 수 있습니다. 쿠키는 도메인별로 저장할 수 있으며 개발자모드(F12)를 활용하면 어떠한 **키/밸류**를 가지고 있는지 확인이 가능합니다.
확인이 가능한 데이터이기에 쿠키는 보안에 취약할 수 밖에 없습니다.
    
다음 세션은 클라이언트와 웹서버간 네트워크 연결이 지속 유지되어있는지를 알기 위하여 사용됩니다.
세션은 **서버**에 저장된 값을 클라이언트에게 전달하는 방식이기때문에 보안성이 쿠키에 비해서 좋습니다.
단, 서버에서 불러오는만큼 쿠키보다는 속도가 느립니다.
쿠키와 세션을 함께 활용하면 보안성이 높은 **로그인 기능**을 구현할 수 있습니다.
쿠키로 세션ID 값을 유지하고 세션ID를 사용하여 서버에서 해당 정보를 가져와 활용할 수 있습니다.
만약 세션이 없다면 아이디, 비밀번호를 쳐서 로그인했더라도 내부 동작함에 있어 매번 사용자 인증을 해야합니다. 예로 시간이 많이 지난 사이트에서 로그인 화면을 다시 요구할 때가 있습니다. 이는 세션이 만료되어 다시 사용자 인증할 필요가 생겼기 때문입니다.
    
### 크로스 브라우징
크로스 브라우징은 웹 표준에 따라 서로 다른 OS 또는 플랫폼에 대응하는 것을 말한다. 브라우저별 렌더링 엔진이 다른 상황 등 어떠한 상황 속에서도 문제 없이 동작하게 하는 것을 목표로 한다. 프론트엔드 개발자는 여러가지 전략을 세울 수가 있는데, feature detection(기능 탐지)을 사용해서 해당 기능이 해당 브라우저에 있는지를 확인하는 방법을 사용할 수도 있다. 특히 한 쪽 환경에 최적화를 하는 것 보다, 전체적인 웹 표준을 지키는 데에 노력해야 한다.
1) 적용 기능의 지원 브라우저 파악 또는 Tool 사용
2) 모든 환경에서 지원해야 한다면 라이브러리를 사용하자
3) 브라우저 표준에 맞게 스타일(CSS) 지원하기
4) Reset.css과 Normalize.css

### Vue.js & React
### CSRF & XSS
-XSS(사이트간 스크립팅)
웹 애플리케이션에서 많이 나타나는 취약점의 하나로, 웹사이트 관리자가 아닌 이가 웹 페이지에 악성 스크립트를 삽입할 수 있는 취약점이다.
이 취약점은 웹 애플리케이션이 사용자로부터 입력 받은 값을 제대로 검사하지 않고 사용할 경우 나타난다. 주로 여러 사용자가 보게 되는 전자 게시판에 악성 스크립트가 담긴 글을 올리는 형태로 이루어진다.
이 취약점으로 해커가 사용자의 정보(쿠키, 세션 등)를 탈취하거나, 자동으로 비정상적인 기능을 수행하게 하거나 할 수 있다. 주로 다른 웹사이트와 정보를 교환하는 식으로 작동한다.
    
-CSRF(사이트간 요청 위조)
웹사이트 취약점 공격의 하나로, 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위(수정, 삭제, 등록 등)를 특정 웹사이트에 요청하게 하는 공격을 말한다.
XSS를 이용한 공격이 사용자가 특정 웹사이트를 신용하는 점을 노린 것이라면, 사이트간 요청 위조는 특정 웹사이트가 사용자의 웹 브라우저를 신용하는 상태를 노린 것이다.
일단 사용자가 웹사이트에 로그인한 상태에서 사이트간 요청 위조 공격 코드가 삽입된 페이지를 열면, 공격 대상이 되는 웹사이트는 위조된 공격 명령이 믿을 수 있는 사용자로부터 발송된 것으로 판단하게 되어 공격에 노출된다.
    
-차이
간단하게, XSS는 공격대상이 Client이고, CSRF는 Server이다.
XSS는 사이트변조나 백도어를 통해 클라이언트에 대한 악성공격을 한다.
CSRF는 요청을 위조하여 사용자의 권한을 이용해 서버에 대한 악성공격을 한다.
