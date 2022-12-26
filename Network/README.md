# Network
1. [OSI 7계층](https://github.com/dltkd1395/CS-study/tree/main/Network#osi-7계층)
2. IP
    1. IPv4
    2. IPv6
    3. 공인 IP, 사설 IP
3. TCP/IP
4. UDP
5. 대칭키 & 공개키
6. Load Balancing
7. Blocking/Non-Blocking & Synchronous/Asynchronous I/O
8. 웹 동작 방식
9. DNS
10. HTTP 프로토콜
11. HTTP와 HTTPS
12. HTTP Method
13. HTTP 상태 코드
14. 쿠키, 세션
15. JWT, OAuth

## OSI 7계층

### OSI 7계층이란
- OSI는 `Open Systems Interconnection`의 약자이다.
- `Open Systems Interconnection`이란, 개방형 시스템 상호연결이다.
</br>

그럼 또 개방형 시스템은 무엇일까?
- 개방형 시스템이란 정해진 규약에 따르기를 원하는 어떠한 업체라도 그 개방형 시스템의 명세(spec.)을 사용하도록 허락된 것이다.(인터페이스를 구현한 클래스와 같은 느낌) 
- 개방형의 반대는 독점적, 폐쇄형이라는 뜻의 Proprietar이다.
</br>
- OSI는 이러한 개방형 시스템들간에 연결이라는 뜻이다.

### 계층을 나눈 이유는?
- 시스템들의 계층을 나눠서 관리하는 이유는 통신이 일어나는 과정을 단계별로 파악할 수 있기 때문이다.
- 흐름을 하눈에 알아보기 쉽고, 사람들이 이해하기 쉽다.
- 또한 계층을 분리함으로서 각 계층은 독립적인 역할을 할 수 있다.
- 독립적으로 자신의 일을 처리하고, 다른 계층으로 interconnection 할 때에 규약을 잘 지키면 되는 방식이다.
- 이렇게 역할이 분리되면서 어떤 한 계층에서 문제가 발생했을 때 다른 계층에 영향을 미치지 않고, 해결할 수 있다.
- 즉, 유지보수가 원활하게 이루어질 수 있다.
- 각 계층은 자신보다 하위 계층을 사용하고 현재 층의 기능을 포함해 상위 계층에 제공한다.
- 자바의 상속과도 비슷하다. 계층구조를 위에서 바라봤을 때 아래쪽은 보이지 않는다. (오버라이딩과 유사)
- 따라서 최상위 계층만 보면 그 하위 계층을 모두 포함하고 있다.

</br>

### 예시

> A 회사에서 개발 1팀의 모든 PC에 문제가 발생했다 -> 라우터의 문제(Network Layer) 이거나, 광랜을 제공하는 회선 문제 (Physical Layer) 이다.
> 반면, A 회사 개발 1팀의 홍길동 씨의 PC에만 문제가 발생했다면 -> 실행한 소프트웨어의 문제 (Application) 이거나, 스위치에 문제 (DataLink)가 있는 것이다.
> 위의 경우들은 해당 계층에 문제가 있다고 판단된다면, 다른 계층은 건들이지 않고 문제가 발생한 계층에서만 해결을 위한 작업을 진행한다.

### OSI 7계층

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/osi1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

### 1st Layer - Physical Layer (물리계층)

- 물리 계층은 말 그대로 `물리적인 하드웨어 전송 기술`들로 이루어져 있다.
- 기계적인 신호를 주고받는 역할로, `비트(0과1) 단위`로 통신한다.
- 전기적, 기계적, 기능적인 특성을 이용해 통신 케이블로 데이터를 전송한다.
- 이 계층은 데이터가 무엇인지, 에러가 발생했는지 전혀 신경쓰지 않으며 오직 데이터를 전송하거나 받기만 한다.
- 데이터를 전기적 신호를 변환해서 주고받는 기능을 한다.

</br>

- 장비
  - 통신 케이블, 리피터, 허브 등
- **케이블, 리피터, 허브를 통해 전기적인 데이터를 전송하는 계층**

### 2st Layer - DataLicnk Layer (데이터 링크 계층)
  
- 데이터 링크 계층에서는 물리 계층에서 송수신되는 데이터의 오류와 흐름을 관리한다.
- 잡음이 있을 수 있는 물리적인 회신을 3계층에서 신뢰적으로 사용할 수 있도록 전송 에러가 없는 채널로 변환시키는 계층이다.

</br>

- 이 계층에서는 `맥 주소`로 통신한다.
- `프레임 단위`로 전송되며 브리지, 스위치 등의 장비를 통해 MAC 주소를 가지고 물리 계층에서 받은 정보를 전달한다.
- `프레임`은 데이터를 전송 단위로 그룹화한 것이다.

</br>

- 데이터 링크 계층은 흐름 제어와 에러 제어를 담당한다.
- 흐름 제어는 데이터를 보내는 측과 받는 측 간의 속도차를 보장하는 것이다.
- 에러 제어는 물리 계층의 전송 오류를 검출하고 수정한다.
- 또한 정확하게 수신되지 않은 패킷들을 재전송한다.

</br>

- 순서화 작업도 담당하는데, 이 작업은 패킷이나 ACK 신호에 일련번호를 부여하는 것이다.
- 데이터 링크 계층은 Point to Point 간 신뢰성있는 전송을 보장하기 위한 계층이다.
- 프로토콜은 HDLC, 이더넷, 무선 LAN, 이동통신, ATM 등 아주 다양하다.

</br>

- 장비
  - 네트워크 브릿지, 스위치
- **물리 계층의 데이터를 에러 검출, 재전송, 흐름 제어, 순서화 등의 작업으로 신뢰적인 프레임을 만들고 프레임에 MAC 주소를 부여해 전송**

### 3rd Layer - Network Layer (네트워크 계층)

- 네트워크 계층에서 가장 중요한 기능은 데이터를 목적지까지 안전하고 빠르게 ㄷ전달하는 기능이다. **(라우팅)**
- 우리가 흔히 아는 IP 주소를 제공하는 계층이며 여기에 사용되는 프로토콜의 종류는 다양하고, 라우팅 방법도 다양하다.
- 라우팅 알고리즘을 통해 경로를 선택해 주소를 정하고 경로에 따라 패킷을 전달한다.
- 주로 라우터를 사용하지만 최근에는 2계층의 장비 중 스위치에 라우팅 기능을 장착한 L3 스위치도 있다고 한다.
- 네트워크 계층으 여러개의 노드를 거칠 떄 마다 경로를 찾아주는 역할을 한다.
- 다양한 길이의 데이터를 네트워크를 통해 전달하고, 그 과정에서 전송 계층이 요구하는 서비스 품질(QoS)를 제공하기 위한 기능적, 절차적 수단을 제공한다.
- 이 계층은 라우팅 (경로 제어), 흐름 제어, 오류 제어 세그멘테이션, 인터네트워킹 등을 수행한다.
- 논리적인 주조 **(IP)**, 즉 네트워크 관리자가 직접 주소를 할당하는 구조를 가지며 계층적이다.

</br>

- 장비
  - 라우터, L3 스위치, IP 공유기 등

- **라우팅으로 최적의 경로를 선택해 패킷을 전송하고 IP 주소를 부여함**

### 4th Layer - Transport Layer (전송 계층)

- 통신을 활성화하기 위한 계층이다. 그래서 가장 핵심적인 계층이며 또한 복잡한 계층이다.
- 보통 TCP 프로토콜을 이용하며, 포트를 열어서 응용 프로그램들이 전송을 할 수 있게 한다.
- 만약 아래 계층에서 데이터를 받았다면 이 계층에서 데이터를 하나로 합쳐서 상위 계층으로 전송한다.

</br>

- 네트워크가 아닌 호스트 내에 구동된 프로세스들 사이에 연결을 확립한다.
- 호스트의 End to End, 양 끝단의 응용 프로세스 상호 간의 통신을 지원한다.

</br>

- 전송 계층은 양 끝단 사이에서 투명한 데이터를 주고 받도록 한다.
- 상위 또는 하위 계층에서 사용하는 제어 방법 및 그 내용에 관계없이 정보가 Session Layer - Transport Layer - Network Layer 간에 내용 바뀜없이 투명하게 전송한다.

</br>

- 전송 계층으 시퀀스 넘버 기반의 오류 제어 방식을 사용한다. 또한 특정 연결의 유효성을 제어한다.
- 일부 프로토콜은 상태가 있고 (stateful), 연결 기반 (connection oriented) 이다.
- 이것은 전송 계층이 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송한다는 뜻이다.

</br>

- 프로토콜
  - TCP, UDP, SCTP 등

- **End to End 통신을 다루는 최하위 계층으로 종단간 신뢰성있고 효율적인 데이터를 전송하며, 오류 검출 및 복구와 흐름 제어, 중복 검사 등을 수행**

### 5th Layer - Session Layer (세션 계층)

- 데이터가 통신하기 위한 논리적인 연결을 말한다. (통신을 하기위한 대문이라고 생각하면 됨)
- 하지만, 바로 아래 계층인 전송 계층에서도 연결을 맺고 종료할 수 있기 때문에 정확하게 어느 게층에서 통신이 끊어졌는지 판단하는 것은 한계가 있다.
- 그래서 세션 계층은 전송 계층과 무관하게 응용 프로그램 관점으로 봐야한다.

</br>

- 주 기능은 세션 결정, 유지, 종료, 전송 중단 시 복구 등이다.
- 세션 계층은 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공한다.
- 동시 송수신 방식 (duplex), 반이중 방식(half-duplex), 전이중 방식 (Full Duplex) 등의 통신이 있으며 체크 포인팅과 유휴, 종료, 다시 시작 과정 등을 수행한다.
- 이 계층은 TCP/IP 세션을 만들고 없애는 책임을 가진다.

- **통신하는 사용자들을 동기화하고 오류 복구 명령들을 일괄적으로 다룸. 통신을 하기 위한 세션을 확립/유지/중단 등을 수행**

### 6th Layer - Pressentation Layer (표현 계층)

- 데이터 표현이 다른 응용 프로세스의 독립성을 제공하고, 암호화한다.

- 표현 계층은 코드 간의 변역을 담당해 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어 준다.
- MIME 인코딩이나 암호화 등의 동작이 이 계층에서 이루어진다.
- 예시로, 문서 파일을 ASCII 인코딩으로 바꾸는 것, 해당 데이터가 TEXT인지 GIF인지 JPG 인지 구분하는 것등의 기능을 수행한다.

- **사용자의 명령어를 완성하고 결과를 표현, 포장/압축/암호화 기능 수행**

### 7th Layer - Application Layer (응용 계층)
  
- 최종 목적지는 HTTP, FTP, POP3 등의 프로토콜이다.
- 통신 패킷들은 위에 나열된 프로토콜에 의해 처리되며 브라우저나 메일은 프로토콜을 쉽게 사용하게 해주는 응용 프로그램이다.
- 즉, 모든 통신의 양 끝은 HTTP와 같은 프로토콜이다 (응용프로그램이 아님)

</br>

- 응용 계층은 응용 프로세스와 직접 관계해 일반적인 응용 서비스를 수행한다.
- 일반적인 응용 서비스는 관련된 응용 프로세스들 사이의 전환을 제공한다.
- 여러 하위 통신 프로토콜 개체에 대해 사용자 관점의 사용자 인터페이스를 제공한다.
- 보통 파일 전송, 메세지 교환 등의 기능을 수행한다.

- 프로토콜
  - HTTP, FTP, SMTP, POP3, IMAP, Telnet 등

- **네트워크 소프트웨어의 UI 부분, 사용자의 입출력(I/O) 부분을 담당**