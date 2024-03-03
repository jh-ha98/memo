# HTTP 웹 기본 정리
## 목차
- [인터넷 네트워크 IP](#인터넷-네트워크-ip)
- [URI & 웹 브라우저 요청 흐름 URI(Uniform Resource Identifier)](#uri--웹-브라우저-요청-흐름-uriuniform-resource-identifier)
- [HTTP 기본 HTTP](#http-기본-http)
- [HTTP 메서드](#http-메서드)
- [클라이언트에서 서버로 데이터 전송](#클라이언트에서-서버로-데이터-전송)
- [HTTP 상태코드](#http-상태코드)
- [HTTP 헤더](#http-헤더)

## [인터넷 네트워크] IP
### IP의 역할
- 지정한 IP 주소(IP Adress)에 데이터 전달
- 패킷(Packet)이라는 통신 단위로 데이터 전달
- IP 패킷 정보 : 출발지 IP, 목적지 IP , 메시지, 기타 ... 

### IP 프로토콜의 한계
비연결성
- 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
- 클라이언트는 대상 서버가 패킷을 받을 수 있는 상태인지 모름

비신뢰성
- 중간에 패킷이 사라질 수 있음(패킷 소실)
- 패킷 전달 순서 문제 발생
- 프로그램 구분
  - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이라면?

### [인터넷 네트워크] TCP
인터넷 프로토콜 스택 4계층
- 애플리케이션 계층 : HTTP, FTP
- 전송계층 : TCP, UDP
- 인터넷 계층 : IP
- 네트워크 인터페이스 계층 : LAN 드라이버, LAN 장비

1) 웹 브라우저가 HTTP 메시지 생성
2) SOCKET 라이브러리를 통해 전달
  - A : TCP/IP 연결(IP, PORT)
  - B : 데이터 전달
3) TCP 정보 생성, HTTP 메시지 포함
4) IP 패킷 생성, TCP 데이터 포함

### TCP 특징
TCP/IP 패키 정보 : 출발지 PORT, 목적제 PORT, 전송 제어, 순서, 검증정보...
<br/>전송 제어 프로토콜
- 연결 지향 - TCP 3 way handshake (가상 연결)
  - SYN : 접속 요청
  - ACK : 요청 수락
  - 연결 과정
    1) SYN
    2) SYN + ACK
    3) ACK (ACK와 함께 데이터 전송 가능)
- 데이터 전달 보증
- 순서 보장
- 신뢰할 수 있는 프로토콜

### UDP 특징
사용자 데이터그램 프로토콜
- 기능이 거의 없음..
- IP와 거의 같음 + PORT + 체크섬 정도만 추가
- 애플리케이션에서 추가 작업 필요

### [인터넷 네트워크] PORT
PORT - 같은 IP 내에서 프로세스 구분
- 0 ~ 65535 할당 가능
- 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
  - FTP : 20, 21
  - TELNET : 23
  - HTTP : 80
  - HTTPS : 443

### [인터넷 네트워크] DNS
도메인 네임 시스템
- 전화번호부
- 도메인 명을 IP주소로 변환

## [URI & 웹 브라우저 요청 흐름] URI(Uniform Resource Identifier)
URI는 로케이터(Locator) , 이름(Name) 또는 둘다 추가로 분류 될 수 있음
- Uniform : 리소스 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier : 다른 항목과 구분하는데 필요한 정보
- URI는 리소스만 식별해야함
- 리소스와 해당 리소스를 대상으로 하는 행위 분리
- URL : Uniform Resource Locator - 리소스가 있는 위치를 지정
- URN : Uniform Resource Name - 리소스에 이름을 부여

### URL scheme
- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
  - 예) http, https, ftp등
- http는 80포트, https는 443포트를 주요 사용, 포트는 생략 가능
- https는 http에 보안 추가 (HTTP Secure)

### URL path
- 리소스 경로(path), 게층적 구조
- 예)
  - /home/file1.png
  - /members

### URL query
  - key=value 형태
  - ?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB
  - query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

### URL fragment
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보 아님

## [HTTP 기본] HTTP
기반 프로토콜
- TCP : HTTP/1.1 , HTTP/2
- UDP : HTTP/3

HTTP 특징
- 클라이언트 서버 구조
- 무상태 프로토콜(Stateless), 비연결성(Connectionless)
- HTTP 메시지
- 단순함, 확장 가능

### 클라이언트 서버 구조
- Request Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답

### 무상태 프로토콜(Stateless)
상태 유지(Stateful)
- 항상 같은 서버가 유지 되어야 함
- 예) 로그인
  - 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
  - 일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지
  - 상태유지는 최소한만 사용

무상태(Stateless)
- 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.
- 무상태는 응답 서버를 쉽게 바꿀 수 있다. -> 무한한 서버 증설 가능
- 스케일 아웃 - 수평 확장 유리
- 예) 로그인이 필요 없는 단순한 서비스 소개 화면

### 비연결성(Connectionless)
- HTTP는 기본이 연결을 유지하지 않는 모델
- 일반적으로 초 단위의 이하의 빠른 속도로 응답
- 서버 자원을 매우 효율적으로 사용할 수 있음

비연결성 한계와 극복
- TCP/IP 연결을 새로 맺어야 함 - 3way handshake 시간 추가
- 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트 , css 추가 이미지 등등 수 많은 자원이 함께 다운로드
- 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결
- HTTP/2, HTTP/3에서 더 많은 최적화

### HTTP 메시지
시작라인

요청 메시지 - HTTP 메서드 
- 종류 : GET, POST, PUT, DELETE
- 서버가 수행해야 할 동작 지정
  - GET : 리소스 조회
  - POST : 요청 내역 처리

요청 메시지 - 요청 대상
- absolute path[?query] (절대경로 [?쿼리])
- 절대경로= "/"로 시작하는 경로
- 참고 : *, http://...?x=y 와 같이 다른 유형의 경로지정 방법도 있다.

요청 메시지 - HTTP version

응답 메시지
- HTTP 버전
- HTTP 상태코드 : 요청 성공, 실패를 나타냄
  - 200 : 성공
  - 400 : 클라이언트 요청 오류
  - 500 : 서버 내부 오류
- 이유 문구 : 사람이 이해 할 수 있는 짧은 상태 코드 설명 글

HTTP 헤더
- header-field = field-name ":" OWS field-name OWS (OWS: 띄어쓰기 허용)
- field-name은 대소문자 구분 없음
- 용도
  - HTTP 전송에 필요한 모든 부가 정보
    - 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라리언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보...
  - 표준 헤더가 너무 많음
  - 필요시 임의의 헤더 추가 가능

HTTP 바디 - 용도
- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

## HTTP 메서드
### 주요 메서드
GET : 리소스 조회
- 서버에 전달하고 싶은 데잍터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
- 메시지 바디를 사용해서 데이터를 전달 할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

POST : 요청 데이터 처리, 주로 등록에 사용
- 메시지 바디를 통해 서버로 요청 데이터 전달
- 서버는 요청 데이터 처리 -> 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행함
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용
- 예) POST /orders/{orderId}/start-delivery (컨트롤 URI)

PUT : 리소스를 대체, 해당 리소스가 없으면 생성
- 클라이언트가 리소스 위치를 알고 URI 지정
- PATCH : 리소스 부분 변경
- DELETE : 리소스 삭제

기타 메서드
- HEAD : GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS : 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
- CONNECT : 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

HTTP 메서드의 속성
- 안전(Safe)
  - 호출해도 리소스를 변경하지 않는다. (해당 리소스만 고려)
- 멱등 (Idempotent)
  - 여러번 호출해도 결과가 똑같다.
  - 자동 복구 메커니즘
  - 외부 요인으로 중간에 리소스가 변경되는 것 까지 고려하지 않음
  - 멱등 메서드 : GET, PUT, DELETE
  - 멱등 X 메서드 : POST
- 캐시가능 (Casheable)
  - GET, HEAD, POST, PATCH는 캐시 가능 하지만 실제로는 GET, HEAD정도만 캐시로 사용
  - POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음

## 클라이언트에서 서버로 데이터 전송
### 쿼리 파라미터를 통한 데이터 전송
- GET
- 주로 정렬 필터(검색어)

### 메시지 바디를 통한 데이터 전송
- POST, PUT, PATCH
- 회원 가입, 상품 주문, 데이터 변경

정적 데이터 조회 : 이미지, 정적 텍스트 문서

동적 데이터 조회 : 주로 검색, 게시판 목록에서 정렬 필터(검색어)

### HTML Form 데이터 전송
HTML Form submit시 POST전송
- 예) 회원 가입, 상품 주문, 데이터 변경

Content-Type : application/x-www-form-urlencoded 사용
- form의 내용을 메시디 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)
- 전송 데이터를 url encoding 처리

Content-Type : multipart/form-data
- 파일 업로드 같은 바이너리 데이터 전송시 사용
- 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능(그래서 이름이 multipart)
- 참고 : HTML Form 전송은 GET, POST만 지원

### HTML API 데이터 전송
- 서버 to 서버(백엔드 시스템 통신)
- 앱 클라이언트(아이폰, 안드로이드)
- 웹 플라이언트
  - HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용(AJAX)
  - 예) React, VueJs 같은 웹 클라이언트와 API 통신
- POST, PUT, PATCH : 메시지 바디를 통해 데이터 전송
- GET : 조회, 쿼리 파라미터로 데이터 전달
- Content-Type : application/json을 주로 사용(TEXT, XML, JSON등)

## HTTP 상태코드
### 2XX - 클라이언트의 요청을 성공적으로 처리
- 200 OK : 요청 성공
- 201 Created : 요청 성공해서 새로운 리소스가 생성됨
- 202 Accepted : 요청이 접수되었으나 처리가 완료되지 않았음
  - 배치 처리 같은 곳에서 사용
  - 예) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함
- 204 No Content : 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음
  - 예) 웹 문서 편집기에서 save 버튼
  - save 버튼의 결과로 아무 내용이 없어도 된다.
  - save 버튼을 눌러도 같은 화면을 유지해야 한다.
  - 결과 내용이 없어도 204 메시지(2XX)만으로 성공을 인식할 수 있다.

### 3XX - 요청을 완료하기 위해 유저 에이전트의 추가 조치 필요
리다이렉션 : 웹 브라우저는 3xx 응답 결과에 Location 헤더가 있으면, Location 위치로 자동 이동
  - 영구 리다이렉션 : 특정 리소스의 URI가 영구적으로 이동, 원래의 URL를 사용X, 검색 엔진 등에서도 변경 인지
    - 301 Moved Permanently : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY) -> 새로운 요청 페이지 
    - 308 Permanent Redirect : 301과 기능은 같음, 리다이렉트시 요청 메서드와 본문 유지(처음 POST를 보내면 리다이렉트도 POST 유지)
  - 일시적인 리다이렉션 : 리소스의 URI가 일시적으로 변경, 검색 엔진 등에서 URL을 변경하면 안됨
    - 주문 완료 후 주문 내역 화면으로 이동
    - 302 Found : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
    - 307 Temporary Redirect : 302와 기능은 같음, 리다이렉트시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안된다. MUST NOT)
    - 303 See Other : 302와 기능은 같음, 리다이렉트시 요청 메서드가 GET으로 변경
    - PRG: Post/Redirect/Get
      - POST로 주문후에 새로 고침으로 인한 중복 주문 방지
      - POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트
      - 새로고침해도 결과 화면을 GET으로 조회
      - 중복 주문 대신에 결과 화면만 GET으로 다시 요청
  - 기타 리다이렉션
    - 304 Not Modified
      - 캐시를 목적으로 사용
      - 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬 PC에 저장된 캐시를 재사용한다. (캐시로 리다이렉트 한다.)
      - 304 응답은 응답에 메시지 바디를 포함하면 안된다. (로컬 캐시를 사용해야 함)
      - 조건부 GET, HEAD 요청시 사용

### 4XX - 클라이언트 오류
클라이언트의 요청에 잘못된 문법등으로 서버가 요청을 수행할 수 없음

오류의 원인이 클라이언트에 있음

중요! 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실패함

- 400 Bad Request : 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음
  - 요청 구문, 메시지 등등 오류
  - 클라이언트는 요청 내용을 다시 검토하고, 보내야함
  - 예) 요청 파라미터가 잘못되거나, API 스펙이 맞지 않을때
- 401 Unauthorized : 클라이언트가 해당 리소스에 대한 인증이 필요함
  - 인증(Authentication) 되지 않음
  - 인증(Authentication) : 본인이 누구인지 확인, (로그인)
  - 401 오류 발생시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명
  - 인가(Authorization) : 권한부여 (ADMIN 권한처럼 특정 리소스에 접근할 수 있는 권한, 인증이 있어야 인가가 있음)
- 403 Forbidden : 서버가 요청을 이해했지만 승인을 거부함
  - 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
- 404 Not Found : 요청 리소스를 찾을 수 없음
  - 요청 리소스가 서버에 없음
  - 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때

### 5XX - 서버 오류
- 500 Internal Server Error : 서버 문제로 오류 발생, 애매하면 500 오류
  - 서버 내부 문제로 오류 발생
- 503 Service Unavailable : 서비스 이용 불가
  - 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음

## HTTP 헤더
### HTTP BODY
- 메시지 본문(message body)을 통해 표현 데이터 전달
- 메시지 본문 = 페이로드(payload)
- 표현은 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더는 표현 데이터를 해석 할 수 있는 정보 제공: 데잍터 유형(html, json), 데이터 길이, 압축 정보 등등
- 참고 : 표현 헤더는 표현 메타데이터와, 페이로드 메시지를 구분해야 하지만, 여기서는 생략

### 표현
Content-Type : 표현 데이터의 형식 설명
  - 미디어 타입, 문자 인코딩 : ex) text/html: charset=utf8, application/json, image/png

content-Encoding : 표현 데이터 인코딩
  - 표현 데이터를 압축하기위해 사용
  - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
  - 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
  -ex) gzip, deflate, identity

Content-Language : 표현 데이터의 자연 언어를 표현 : ex) ko, en, en-US

Content-Length : 표현 데잍의 길이 
  - 바이트 단위
  - Transfer-Encoding (전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

### 콘텐츠 협상
협상(콘텐츠 네고시에이션) - 클라이언트가 선호하는 표현 요청
- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어

협상 헤더는 요청시에만 사용

협상과 우선순위1 (Quality Values(q))
- Quality Values(q) 값 사용
- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
  - 1. ko-KR;q=1 (q생략)
  - 2. ko;q=0.9
  - 3. en-US;q=0.8
  - 4. en;q=0.7

협상과 우선순위2 (Quality Values(q))
- 구체적인 것이 우선
- Accept: text/*, text/plain, text/plain;format=flowed, \*\/\*
  - 1. text/plain;format=flowed
  - 2. text/plain
  - 3. text/*
  - 4. \*\/\* 

협상과 우선순위3 (Quality Values(q))
- 구체적인 것을 기준으로 미디어 타입을 맞춘다.
- Accept: text/*;q=0.3, text/html;q=0.7, text/html;level=1, text/html;level=2;q=0.4, \*\/\*;q=0.5

### 전송방식
단순전송 : 콘텐츠의 길이를 알 수 있을 때
- Content-Length

압축전송
- Content-Encoding : gzip
- Content-Length

분할전송
- Content-Type : text/plain
- Transfer-Encoding : chunked
- Content-Length는 넣으면 안됨

범위전송
- Range, Content-Range 

### 일반정보
From : 유저 에이전트의 이메일 정보
- 일반적으로 잘 사용되지 않음
- 검색 엔진 같은 곳에서, 주로 사용
- 요청에서 사용

Referer : 이전 웹 페이지 주소
- 현재 요청된 페이지의 이전 웹 페이지 주소
- A -> B로 이동하는 경우 B를 요청할 때 Referer: A 를 포함해서 요청
- Referer를 사용해서 유입 경로 분석 가능
- 요청에서 사용
- 참고: referer는 단어 referrer의 오타

User-Agent : 유저 에이전트 애플리케이션 정보
- user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/
537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
- 클라이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)
- 통계 정보
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- 요청에서 사용

Server : 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
- ORIGIN 서버 : 원본 파일이 저장되는 곳, 들어오는 인터넷 요청을 수신 대기하고 처리하도록 설계된 하나 이상의 프로그램을 실행하는 컴퓨터 
- Server: Apache/2.2.22 (Debian)
- server: nginx
- 응답에서 사용

Date : 메시지가 발생한 날짜와 시간
- Date: Tue, 15 Nov 1994 08:12:31 GMT
- 응답에서 사용

### 특별한 정보
Host : 요청한 호스트 정보(도메인) -> 필수 !
- 요청에서 사용
- 하나의 서버가 여러 도메인을 처리해야 할 때
- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때

Location : 페이지 리다이렉션
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동
(리다이렉트)
- 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
- 3xx (Redirection): Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴

Allow : 허용 가능한 HTTP 메서드
- 405 (Method Not Allowed) 에서 응답에 포함해야함
- Allow: GET, HEAD, PUT

Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
- 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
- Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
- Retry-After: 120 (초단위 표기)

### 인증
Authorization : 클라이언트 인증 정보를 서버에 전달
- Authorization: Basic xxxxxxxxxxxxxxxx

WWW-Authenticate : 리소스 접근시 필요한 인증 방법 정의
- 리소스 접근시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용
- WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"