---
layout: single
title: "📝 웹서비스 프로그래밍 중간고사 정리"
toc: true
toc_sticky: true
toc_label: "웹서비스 프로그래밍 1~6장, 세션, 쿠키, 시큐어코딩"
categories: webservice
excerpt: "2022-10-26 웹서비스 프로그래밍 중간"
tag: [middle test]
---

# CHAP.01 웹 프로그래밍의 이해

## 1. 웹의 개요

### 웹이란?

- World Wide Web(WWW)

  - 인터넷에서 운영되는 서비스 중 하나로 웹 자체가 인터넷을 의미하는 것은 아님
  - 웹의 개발 목적
    - 연구자들이 흩어져 있는 정보를 손쉽게 정리하고 공유하기 위함

- 웹의 특징
  - 인터넷은 컴퓨터 네트워크 망, 웹은 인터넷 서비스 중 하나를 의미함
  - 인터넷 상의 정보를 하이퍼텍스트<sup>_참조(하이퍼링크)를 통해 독자가 한 문서에서 다른 문서로 즉시 접근 할 수 있는 텍스트_</sup> 방식과 멀티미디어 환경에서 검색할 수 있게 해주는 검색 시스템
  - HTTP 프로토콜 사용
  - HTML 문서를 연결하여 다양한 컨텐츠 제공
  - 많은 사람들이 정보를 쉽게 공유하고 접근할 수 있도록 하는것을 목적으로 함

### 웹의 동작 구조

<!-- ![image](../../images/2022-10-25-webservice/215702.png){: .align-center} -->

<img src="../../images/2022-10-25-webservice/215702.png" style="box-sizing: border-box; width: 80%; display: block;
  margin-left: auto;
  margin-right: auto;">

- HTML을 중심으로 한 웹의 동작 과정
  1. URL 입력
  2. DNS 서버에서 도메인 이름을 IP주소로 변환하여 제공
  3. IP 주소의 서버 80번 포트로 접속 시도(서버는 접속 대기)
  4. 웹 서버는 요청 내용을 분석하여 해당 페이지를 읽음
  5. 웹 서버는 HTML 파일 내용을 텍스트로 클라이언트로 전송
  6. 웹 브라우저는 HTML 태그를 분석하고 적절히 변환하여 화면 구성

## 2. 네트워크와 인터넷 개념

### 네트워크

- 네트워크(Network)

  - 컴퓨터와 컴퓨터를 연결해주는 망

- 프로토콜(Protocol)

  - 네트워크를 구축하기 위한 컴퓨터 간의 연결 규격
  - TCP/IP : 여러 프로토콜 중 가장 널리 쓰이며 인터넷에서도 사용되고 있는 프로토콜

- TCP/IP(Transmission Control Protocol/Internet Protocol)
  - 컴퓨터 간에 통신할 수 있도록 만든 프로토콜의 종류 중 한가지
  - 인터넷은 이 프로토콜에 기반함
    - 하드웨어, 운영체제, 접속 매체와 관계없이 동작 할 수 있는 개방형 구조
- OSI 7계층
  - 네트워킹을 위한 물리적 장비에서부터 실제 서비스를 제공하기 위한 어플리케이션에 이르는 단계 까지를 계층화한 모델
  - 계층화를 통해 상위 레벨에서는 하위 레벨에서 구현한 내용을 모르더라도 표준화된 인터페이스를 통해 네트워크 시스템을 개발, 운영 할 수 있음
- TCP/IP의 특징

  - OSI 7계층을 좀 더 단순화 하여 4계층으로 정의
  - TCP: 데이터 흐름관리, 데이터 정확성 확인 등의 역할 수행
  - IP: 데이터(패킷)를 목적지까지 전송하는 역할 담당
  - TCP/IP는 개방형 구조로, 특정 운영체제나 하드웨어에 영향을 받지 않고 근거리와 원거리 모두 데이터를 전송 할 수 있음

- IP주소(IP Address)
  - TCP/IP로 연결된 네트워크에서 각각의 컴퓨터를 구별하기 위해 사용하는 주소

### 인터넷

- 포트(Port)

  - 네트워크 서비스를 제공하기 위한 일종의 출입문
  - 하나의 컴퓨터에서 여러개의 네트워크 서비스를 제공하는 경우, 이들을 구분하기 위한 목적으로 사용
    - ex) 은행에서 입출금, 대출 등 업무에 따라 창구를 구별
  - 포트와 프로토콜이 일치하지 않는 경우 정상적인 네트워크 서비스를 이용할 수 없음
  - 포트는 접속할 수 있게 개방해 놓은 문과 같으므로 보안과 밀접한 관계가 있음

- DNS(Domain Name System)
  <img src="../../images/2022-10-25-webservice/221409.png" style="box-sizing: border-box; width: 100%; display: block;
    margin-left: auto;
    margin-right: auto;">

  - 컴퓨터의 IP주소는 네트워크에서 컴퓨터를 구분해주는 주민번호같은 개념
  - 인터넷 주소의 형태: 호스트(computer)이름(www) + 도메인 이름(kim-song-jun.github.io)
  - 도메인 이름은 규칙에 따라 붙여지며, 도메인을 관리하는 기관에 일정 비용을 지불하고 구매해야 함
  - 도메인 이름을 통한 웹 사이트 접속도 결국 내부적으로 도메인 이름을 IP주소로 변환하는 서비스 이용

## 3. 웹 프로그래밍의 구조

### 클라이언트-서버 구조

- 클라이언트-서버 구조

  - 웹 서비스 제공을 위해서는 서버 컴퓨터와 서버에서 동작하는 프로그램이 필요함
    <img src="../../images/2022-10-25-webservice/221716.png" style="box-sizing: border-box; width: 100%; display: block;
      margin-left: auto;
      margin-right: auto;">

  - 클라이언트
    - 웹 서비스를 이용하는 사용자(Web Browser: Client Program)
  - 서버
    - 웹 서비스를 제공하기 위한 서비스 공급자

### HTML/CSS/JS

- HTML(HyperText Markup Language)
  - 웹 문서의 구조를 정의하고 컨텐츠를 표현하는 기본 마크업 언어
  - 웹을 통해 컨텐츠를 제공하려면 HTML을 사용해야 함
  - HTML은 테그라고 하는 간단한 표기법으로 표현하고자 하는 정보에 의미 부여
- CSS(Cascading Style Sheet)

  - HTML 문서에 레이아웃과 디자인을 포함한 시각적 요소 정의
  - HTML은 컨텐츠의 내용과 구조(Layout)를 정의하고 CSS에서 컨텐츠의 위치, 정렬, 글자크기, 여백, 색상 등을 정의
  - 디자인을 적용할 HTMl 요소를 셀렉터(Selector)<sup>_ID, class, tag_</sup>로 지정하고 원하는 디자인 속성을 부여하는 형식 사용

- JS
  - HTML 문서의 동적으로 변하는 컨텐츠를 표현하기 위해 이벤트 처리를 하거나 서버와 연결하여 데이터를 가지고 오는 등의 역할을 하는 프로그램 언어
  - HTML 문서에서 이벤트를 서버 연결 없이 동적으로 처리할 수 있는 기술

### BE 중심 개발과 FE 중심 개발

- BE 중심 개발

  - 전통적인 웹 개발 모델, 서버에서 모든걸 담당함
  - Java Servelt/JSP는 가장 인기있는 BE 기술
    <img src="../../images/2022-10-25-webservice/222423.png" style="box-sizing: border-box; width: 100%; display: block;
           margin-left: auto;
           margin-right: auto;">
    1. Client 요청은 URL 형태로 수행
    2. Servelt/Java or Node.js 등을 사용해 DB 연동
    3. JSP에서 HTML과 데이터를 조합하여 페이지 구성
    4. Client에 HTML 형태의 응답 전달

- BE 중심 개발 장점

  - 서비스 연동에 필요한 다양한 서버 환경에 대응 가능(SSR)
  - SEO 최적하 유리
  - 기술이 안정적/검증됨
  - 기존에 개발된 시스템이 많고 Legacy System<sup>_낡은 시스템_</sup>은 오랫동안 유지됨

- BE 중심 개발 단점

  - Mobile Network의 속도가 느리며 많은 비용을 지불해야함
  - 서버에 화면 갱신을 요청할 경우 모든 데이터가 다시 전송되어야함<sup>모바일에 부적합</sup>
  - REST API와 클라우드 인프라가 보편화 되면서 기존에 대규모로 서버를 구축하는 모놀리식 아키텍처 방식보다는 소규모 서버를 연동하는 MSA(Micro Service Architecture) 방식 확산

- FE 중심 개발

  - Client에서 HTML을 가지고 있거나, Server에서 HTML만 받아오고, 서버로부터 화면 구성에 필요한 Data만 js로 받아와 Data와 화면을 조합해 보여줌(CSR)
    <img src="../../images/2022-10-25-webservice/223122.png" style="box-sizing: border-box; width: 100%; display: block;
             margin-left: auto;
             margin-right: auto;">

  1. Client 요청은 URI<sup>_화면, 데이터를 가져오기 위한 서버 프로그램과 파라미터를 포함하는 개념, URL보다 큰 개념_</sup> 형태로 수행
  2. Java Servelt, JAX-RS, Node.js 등을 통해 DB와 연동
  3. Client에 Json 형태의 응답 전달
  4. Client는 전달받은 Json Data를 HTML과 조합(rendering)

- FE 중심 개발의 장점
  - 필요한 부분의 데이터 갱신이 가능하기 때문에 서버로부터 매번 갱신된 HTML를 받아 올 필요가 없음
  - 실시간 데이터 갱신이 자유로움
  - SPA, PWA등의 구현에 적용 가능
- FE 중심 개발의 단점
  - FE 중심이더라도 Data 제공을 위한 Server는 필요
  - Data 제공 서버는 주로 REST API로 개발되기 때문에 BE 작업은 당연히 존재
  - SEO 최적화를 위해 SSR를 접목하기도 함

# CHAP.02 자바 웹 개발을 위한 환경 구축

## 1. 자바 웹 개발환경의 개요

### 자바란?

- 자바의 특징

  - 간결하면서고 강력한 객체지향 프로그래밍 언어
  - 플랫폼 독립적
  - 많은 오픈소스 라이브러리를 이용한 생산성 향상, 유지보수 비용 절감
  - GUI/하드웨어 프로그램 개발에는 비교적 부적합
  - Modern Laguage보다 간결함이 떨어지고 복잡함

- JVM(Java Virtual Machine)

  - 자바의 가장 큰 특징을 타나내는 개념
  - 물리적인 기계 장치가 아닌 가상의 세계
    - 소프트웨어로 구현된 하드웨어를 의미함
    - 임베디드 개발을 위해 고안된 아이디어였음
  - 플랫폼 독립적
    <img src="../../images/2022-10-25-webservice/223912.png" style="box-sizing: border-box; width: 100%; display: block;
               margin-left: auto;
               margin-right: auto;">
  - 자바 소스는 컴파일 이후 byte 코드가 생성되고, JVM은 byte 코드를 해석하여 운영체제에서 실행 할 수 있도록 번역하는 역할 담당

- 자바 플랫폼
  - API와 JVM으로 구성되며 특정 자바 프로그램이 실행되는 환경을 의미함
  - Java SE, EE, ME, Card, TV 등이 있음
  - 실행 환경에 따라 API 구성등이 달라짐
    - 일반적으로 SE 설치
    - 대규모 개발 EE 추가 설치

### 자바 웹 개발환경

- 자바 웹 개발을 위한 환경
  - 자바 실행 환경(JRE - JDK로 설치)
  - 통합 개발 환경(IDE - 컴파일러, 디버거, API, 편집기 등 포함)
  - 서블릿 컨테이너
  - DB

|         요소         | 프로그램 명 |                                                        목적                                                        |
| :------------------: | :---------: | :----------------------------------------------------------------------------------------------------------------: |
|    자바 개발 도구    |     JDK     |                            JSP는 HTML내에 자바 코드를 작성하기 때문에 JDK가 반드시 설치                            |
|    통합 개발 환경    |   Eclipse   |                                                 대표적인 자바 IDE                                                  |
| 서블릿 컨테이너(WAS) | 아파치 톰캣 | 웹 어플리케이션이 서버에서 실행되기 위해서는 서블릿 컨테이너가 설치되어야 함<br> 톰캣, Jetty, Undertow 등이 사용됨 |
|          DB          |    MySQL    |                                                   ER데이터베이스                                                   |

- JDK(Java Development Kit)

  - JDK는 JRE와 컴파일러등을 포함
  - IDE를 비롯해 톰캣과 같이 자바로 만들어진 서버 실행을 위해서도 JDK가 필요

- IDE(Integrated Development Environment)

  - 이클립스 등

- 서블릿 컨테이너(Web Application Server, WAS)
  - 웹 어플리케이션을 구동하는 서버
  - 서버가 WAS로 동작하려면 서블릿 컨테이너 필요
  - 실제 서비스 시스템을 구축할때는 정적 콘텐츠 서비스를 위한 웹 서버와, WAS를 병행해 운영하며 설정을 통해 상호 연동되는 구조
  - 톰캣, jetty, undertow 등이 있음
  - 서블릿 컨테이너 구조
    <img src="../../images/2022-10-25-webservice/225729.png" style="box-sizing: border-box; width: 100%; display: block;
                 margin-left: auto;
                 margin-right: auto;">

## 2. 클라우드 개발환경과 배포 프로세스

### 클라우드 개발 환경

- 클라우드 인프라 협업을 위한 기본적인 배경지식과 경험이 요구됨
- 개발환경이 복잡해짐 -> 결과물을 서버로 배포하는 과정, 절차도 복잡해짐
- 클라우드 개발 환경에 대한 어느정도의 이해 필요

### 배포 프로세스

- 배포(Deployment)

  - 배치라고도 하며, 개발된 결과물을 실제 사용자에게 전달하는 작업
  - Web
    - 운영 서버로 소스코드를 복사하고 WAS에 등록하는 과정
  - Mobile
    - 앱 스토어에 앱을 업로드 하는 절차 등
  - 그 외
    - FTP서버, 홈페이지 or github 등을 통해 버전을 Release하는 작업 등

- Web Application 배포

  - 이클립스에서 JSP or Servelt을 실행하면 현재 프로젝트 구조를 .war로 패키징 후 톰캣에 전달해 실행하는 구조
  - 운영 서버에 설치하는 경우, .war 파일을 서버에 옮기는 과정 필요
  - 비효율 적이며 불편한점이 많음
    - DebOps라 불리는 개발, 운영 통합 인프라 스트럭처 사용

- DevOps

  - 개발(Development)과 운영(Operation)의 합성어
  - 규모가 큰 소프트웨어의 신속한 개발과 지속적인 유지보수, 배포 등의 운영을 병행하기 위한 노력
  - 빈번한 서비스 배포, 웹 기반의 서비스 형태가 필수 요소로 자리잡음
  - 이러한 새로운 전략을 위해 개발팀과 운영팀이 병합되어
    - 개발, 테스트 배포, 운영에 이르는 어플리케이션 생명주기 개발

- DevOps 장점

  - 빠른 속도
    - 계획부터 배포까지 작업 속도를 빠르고 효율적으로 제공
    - 시장변화에 빠르게 대처하고 비지니스 성과 창출 가능
  - 빠른 배포
    - 새로운 기능의 릴리즈와 오류 수정 속도가 빨라져 고객의 요구에 빠르게 대응
  - 안정성
    - 지속적 통합, 지속적 전달, 모니터링, 로깅을 통해 안정적인 서비스 품질 제공
  - 확장 가능성
    - 복잡하거나 변화하는 시스템을 효율적으로 관리
  - 협업 강화
    - 개발 팀과 운영 팀의 긴밀한 협력, 책임 공유 -> 비효율을 줄이고 시간 절약

- DevOps의 구성요소
  - SCM(Source Code Management)
    - 팀 단위의 소스코드 버전 관리; git, SVN등의 tool 사용
  - CI(Continuous Integration)
    - build와 test 통합; Jenkins, Travis CI 등의 도구 사용
  - CD(Continuous Deploy)
    - 지속적인 배포, 원하는 시점에 바로 배포가 가능한 설정 필요
  - CM(Configuration Management)
    - 서비스 설정의 통합 관리, 운영서버 OS, 라이브러리 버전, 컴파일 등 포함
