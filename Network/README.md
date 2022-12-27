# Network
1. [OSI 7계층](https://github.com/dltkd1395/CS-study/tree/main/Network#osi-7계층)
2. [IP](https://github.com/dltkd1395/CS-study/tree/main/Network#ip)
    1. [IPv4](https://github.com/dltkd1395/CS-study/tree/main/Network#ipv4)
    2. [IPv6](https://github.com/dltkd1395/CS-study/tree/main/Network#ipv6)
    3. [공인 IP, 사설 IP](https://github.com/dltkd1395/CS-study/tree/main/Network#공인-ip-사설-ip)
3. [TCP/IP](https://github.com/dltkd1395/CS-study/tree/main/Network#tcpip)
4. [UDP](https://github.com/dltkd1395/CS-study/tree/main/Network#udp)
5. [대칭키 & 공개키](https://github.com/dltkd1395/CS-study/tree/main/Network#대칭키-공개키)
6. [Load Balancing](https://github.com/dltkd1395/CS-study/tree/main/Network#load-balancing)
7. [Blocking/Non-Blocking & Synchronous/Asynchronous I/O](https://github.com/dltkd1395/CS-study/tree/main/Network#blocking-vs-non-blocking-io-%EC%99%80-synchronous-vs-asynchronous-io)
8. [웹 동작 방식](https://github.com/dltkd1395/CS-study/tree/main/Network#웹-동작-방식)
9. [DNS](https://github.com/dltkd1395/CS-study/tree/main/Network#dns)
10. [HTTP 프로토콜](https://github.com/dltkd1395/CS-study/tree/main/Network#http-프로토콜)
11. [HTTP와 HTTPS](https://github.com/dltkd1395/CS-study/tree/main/Network#http와-https)
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
- 개방형의 반대는 독점적, 폐쇄형이라는 뜻의 Proprietary이다.
</br>
- OSI는 이러한 개방형 시스템들간에 연결이라는 뜻이다.

### 계층을 나눈 이유는?
- 시스템들의 계층을 나눠서 관리하는 이유는 통신이 일어나는 과정을 단계별로 파악할 수 있기 때문이다.
- 흐름을 한눈에 알아보기 쉽고, 사람들이 이해하기 쉽다.
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

- 네트워크 계층에서 가장 중요한 기능은 데이터를 목적지까지 안전하고 빠르게 전달하는 기능이다. **(라우팅)**
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

- 전송 계층은 시퀀스 넘버 기반의 오류 제어 방식을 사용한다. 또한 특정 연결의 유효성을 제어한다.
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

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

---



### IP


### IPv4

### IPv4 Protocol

- IPv4 Protocol은 `비신뢰적`이고 `비연결형`인 `최선형 전송` 서비스이다. `최선형 전송`의 의미는 IPv4 패킷이 유실되거나 순서에 맞지 않게 도착할 수 있다는 뜻이다.
- 만약 신뢰성이 중요하다면 IPv4는 TCP와 같은 신뢰성 있는 전송 계층 프로토콜과 함께 사용되어야 한다. 

</br>

### IPv4 Datagram

- IPv4의 Datagram은 가변 길이의 패킷으로, Header와 Payload(Data)로 이뤄져 있다.
- Header는 20에서 60바이트의 길이이며 라우팅과 같은 전송과 관련한 정보를 가지고 있다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/ip1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

[출처](https://electronicspost.com/ipv4-datagram-format/)

- IPv4의 각 필드의 기능은 다음과 같다


필드 | 기능
|---|---|
Version | IP 프로토콜의 버전을 의미하며, IPv4는 4의 값을 가진다.
Header length | IPv4 Datagram은 가변의 Header를 가지며, 수신자는 전체 길이를 확인하기 위하여 필드 값에 4를 곱한다.
Type of service | 8-bit로 구성되며, Datagram이 라우터에 의해 어떻게 처리되어야 할지 정의한다.
datagran length (byte) | 16-bit의 필드는 IP Datagram의 전체 바이트 크기를 의미한다.
16-bit Identifiler, Flags, 13-bit Fragmentation offset | 이 세 필드는 Datagram의 크기가 하부 네트워크가 처리할 수 있는 크기보다 클 경우에 필요한 IP Datagram의 단편화와 관련이 있다.
Time-to-live | Datagram이 방문할 수 있는 최대 라우터의 수를 의미한다.
Upper-layer Protocol | Datagram이 목적지에 도착하면 어느 프로토콜로 Payload가 전달되어야 할지 알려준다.
Header checksum | IP는 Header를 검사하기 위한 checksum 필드를 사용하고 있다.
32-bit SOurce IP address, 32-bit Destination IP address | 이 필드는 32-bit 길이의 추ㅜㄹ발지, 목적지 주소를 의미한다.
Options (if any) | Datagram Header는 40바이트까지 옵션을 가질 수 있다. 옵션은 필수가 아니지만, 옵션을 사용할 때 이 필드가 사용된다.
data | 이 필드는 Payload(Data)를 의미한다.

### IPv4 주소

- IPv4 주소는 오늘날 대중적으로 사용되는 IP 주소이다.

진법 | IP Address
|---|---|
2진법 | 11000000 10101000 00000000 00000001
10진법 | 192.168.0.1
16진법 | C0 A8 00 01

- IPv4 주소는 32-bit 주소 체계로 위와 같이 표기할 수 있는데, 일반적으로 10진수와 '.'를 이용하여 표한한다.
- 10진수로 표기할 경우 8비트씩 끊어서 사용하므로 0 ~ 255 범위의 숫자를 사용하여 표현할 수 있다.

### IPv4 특수 주소

- IPv4에는 특수 용도로 사용되는 주소들이 있다.

특수 주소 | 기능
|---|---|
Loopback | 127.0.0.8/8 주소는 루프백 주소이다. 이 주소를 가진 패킷은 호스트를 떠나지 않고, 호스트에 남게 된다. 테스트 용도로 많이 사용되며 그 중 127.0.0.1 주소는 테스트에 가장 많이 사용되는 주소이다.
Limited-broadcast | 255.255.255.255/32 주소는 제한된 브로드캐스트 주소이다. 이 주소를 통해 호스트나 라우터가 네트워크 상의 모든 장치로 데이터를 보낼 수 있다. 하지만 대부분의 라우터에는 이러한 패킷을 차단하기 때문에 외부로는 보낼 수 없다.
This-host | 0.0.0.0/32 주소는 디스-호스트 주소이다. 이 주소는 현재 네트워크를 의미하며, 자신의 주소를 모를 때 사용되는 주소이다.
Private | 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 주소는 사설 주소로 지정되어 있다. 이러한 주소들은 공공 인터넷에 존재하지 않으며 사설로만 사용이 가능하다.
Multicast | 224.0.0.0/4 주소는 멀티캐스트 용도로 사용되는 주소이다.

### IPv6

### IPv6 Protocol

- IPv6 Protocol은 IPv4의 주소 고갈, IP 패킷의 형태 변경, ICMP와 같은 몇몇 보조 프로토콜의 수정을 위해 고안된 새로운 버전의 프로토콜이다.

### IPv6 Datagram

- IPv6 Datagram은 Header와 Payload로 구성된다.
- 기본 Header는 40바이트를 차지하며, 확장 Header와 상위 계층 Data는 65,535바이트까지의 정보를 가질 수 있다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/ip2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

[출처](https://electronicspost.com/ipv6-datagram-format/)

- IPv6의 각 필드의 역할은 다음과 같다.

필드 | 기능
|---|---|
Version | IP의 버전 전호를 의미합니다. IPv6에서는 6의 값을 가집니다.
Traffic class | IPv4의 Type of service 필드와 유사합니다.
Flow label | Data의 특정한 프름을 위한 특별한 처리를 제공하기 위해 사용됩니다.
Payload length | 기본 Header를 제외한 IP Datagram의 길이를 의미합니다. IPv6의 기본 Header의 길이는 40바이트로 고정되어 있기 때문에 페이로드의 길이만 정의하면 됩니다.
Next hdr | Next hdr 필드는 첫 확장 Header의 종류를 정의하거나 Datagram의 기본 Header를 뒤따르는 Header를 의미합니다. 이 필드는 IPv4의 Upper-layer Protocol 필드와 유사합니다.
Hop limit | IPv4의 Time-to-live 필드와 같은 목적으로 사용됩니다.
Source address (128bits), Destination address (128bits) | 출발지, 목적지 주소를 식별하기 위해 사용됩니다.
Data | IPv4와 달리 IPv6의 Data(Payload) 필드는 다른 형태와 의미를 가집니다.

### IPv6 Datagram Payload(Data 필드)

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/ip3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

[출처](https://www.cisco.com/en/US/technologies/tk648/tk872/technologies_white_paper0900aecd8054d37d.html)

- IPv6 패킷은 기본 Header와 확장 Header로 구성된다. 기본 Header의 길이는 40바이트로 고정되어 있지만, 부가적인 기능을 제공하기 위해 기본 Header 뒤에 6개까지 확장 Header를 붙일 수 있다.
  - Hop-by-hop
  - Destination
  - Source Routing
  - Frgmentation
  - Authentication
  - ESP

### IPv6 주소

- IPv6는 IP 주소가 부족해짐에 따라 새롭게 고안된 IP 주소 체계이다. 기본의 32-bit의 주소는 128-bit로 확장되었다.
- 오늘날 네트워크 기능을 가지는 장비(L3 Router, L4 Switch, PC, Server 등)들의 대부분은 IPv4 주소를 모두 지원하고 있으며, 천천히 IPv6 주소체계로 전환을 하고 있다.

진법 | IP Address
|---|---|
2진법 | 1111111011110110 ... 1111111100000000
16진법 | FEF6:BA98:7654:46E0:AFFF:F210:1124:00F1

- 16진법으로 표현된 IPv6 주소는 많은 수의 0을 포함하고 있어 매우 긴 형태를 보이고 있다.
- 이러한 경우 앞 부분의 0을 생략하고 축약된 표현을 사용할 수 있다. 0082는 82, 0FFE는 FFE, 0000은 0으로 표현할 수 있다.
- 연속되는 영역이 0으로만 구성되어 있다면, 더많은 축약이 가능하다.

> FFFF:0:0:0:EEEE:AAAA:BBBB -> FFFF::EEEE:AAAA:BBBB

- 위 축약은 주소당 한 번만 가능하며, 0만을 가지는 연속된 영역이 두 개 이상 존재할 경우 한 부분만 축약이 가능하다.

### 공인 IP, 사설 IP

### 공인 IP

- 인터넷 서비스 공급자(ISP)가 제공하는 IP 주소로 공용 IP 주소라고도 불리며 `외부에 공개되어 있는 IP`
- 전세계에서 유일한 IP를 가진다.
- 공인 IP 주소가 외부 공개되어 있기 때문에 인터넷에 연결된 다른 PC로부터의 접근이 가능하다. 따라서 공인 IP주소를 사용하는 경우에는 방화벽이나 보안 프로그램을 설치할 필요가 있다.

### 사설 IP
  
- 일반 가정이나 회사 내 등에 할당된 네트워크의 IP 주소로 로컬 IP, 가상 IP라고도 한다.
- `IPv4의 주소 부족`으로 인해 서브넷팅된 IP이기 때문에 라우터에 의해 로컬 네트워크 상의 PC나 장치에 할당된다.
</br>

- 전체 IP 대역 중에서 다음의 대역은 사설 IP 대역으로 설정되어 있기 때문에 사용자가 임의로 부여하고 사용할 수 있으며 인터넷 상에서 서로 연결되지 않도록 되어 있다.

구분 | 범위
|---|---|
A 클래스 | 10.0.0.1 ~ 10.255.255.255
B 클래스 | 172.16.0.1 ~ 172.31.255.255
C 클래스 | 192.168.0.1 ~ 192.168.255.255

- 사설 IP로 회사나 가정 내의 IP 주소를 부여하고 공유기 등에 고정 IP를 부여한 다음에 인터넷에 접속하는 방식이 널리 퍼지게 되었고, 대부분의 장비가 현재는 사설 IP를 부여하고 공유기를 통해 인터넷에 접속하게 된다.
  - 공유기는 공인 IP를 가진다
  - 컴퓨터나 노트북은 사설 IP를 가지고 공유기를 통해 인터넷에 접근할 수 있다.

### 사설 IP와 공인 IP의 차이

| | 공인 IP | 사설 IP  
|---|---|---|
할당 주체 | ISP(인터넷 서비스 공급자) | 라우터(공유기)
할당 대상 | 개인 또는 회사의 서버(라우터) | 개인 또는 회사의 기기
고유성 | 인터넷 상에서 유일한 주소 | 하나의 네트워크 안에서 유일
공개 여부 | 내/외부 접근 가능 | 외부 접근 불가능

### NAT 
- Network Address Translation의 약자로 OSI 3계층인 네트워크 계층에서 공인 IP와 사설 IP로 변환하는 역할을 한다.
- IPv4의 주소 부족으로 인해 공인 `IP 주소를 절약`하고 외부로부터 침입을 차단하기 위해 사용한다.

NAT에는 Basic NAT와 NAPT 2 종류가 있고 대개 NAT라고 하면 NAPT 방식을 말한다.

### NAPT

- Network Address Port Translation의 약자로 사설 IP 주소를 가지는 여러 대의 단말이 하나의 공인 IP 주소를 통해 인터넷과 연결되는 방식
- 공인 IP 주소 절약을 목적으로 사용되며 1:N Translation 규칙을 사용한다. (1 = 공인 IP, N = 사설 IP)
- NAPT 방식을 이용하면 간략하게 아래와 같이 인터넷과 연결된다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/ip4.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

[출처](https://netmanias.com/ko/?m=view&id=blog&no=5826)

(사설 IP -> 공인 IP)
1. 사설 IP 주소를 가진 단말이 인터넷으로 전송하고자 하면 사설 IP와 Port에 대한 공인 IP와 Port를 할당하고 NAT Binding Table에 해당 정보를 생성한다.
2. NAT Binding Table을 참조해서 사설 IP 주소를 공인 IP 주소로 변환하고 인터넷으로 전송한다.

(공인 IP -> 사설 IP) </br>
3. NAT Binding Table을 참조해서 공인 IP 주소를 사설 IP 주소로 변환해서 단말로 전송한다.

### 고정 IP
- 컴퓨터에 고정적으로 부여된 IP
- 한번 부여되면 반납하기 전까지 다른 장비에 부여할 수 없는 IP 주소
- 인터넷에서 서버를 운영하고자 할 때는 공인 IP를 고정 IP로 부여해야 한다. 공인 IP를 부여받지 못하면 다른 사람이 내 서버에 접속할 수 없고, 고정 IP를 부여하지 않으면  내 서버가 아닌 다른 사람의 서버로 접속할 수 있다.

### 유동 IP
- 장비에 고정적으로 IP를 부여하지 않고 컴퓨터를 사용할 때 남아 있는 IP 중에서 돌아가면서 부여하는 IP

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

### TCP/IP

- `TCP/IP` 는 하나의 프로토콜이 아닌 TCP 프로토콜과 IP 프로토콜을 합쳐서 부르는 말이다.
- **패킷 통신 방식의 인터넷 프로토콜인 IP와 전송조절 프토토콜인 TCP**로 이루어져 있다.
- `IP`는 패킷 전달 여부는 보증하지 않고 논리적인 주소만을 제공하며, 패킷을 보낸 순서와 받는 순서가 보장되지 않는다.
- `TCP`는 IP 위에서 동작하는 프로토콜로 데이터의 전달을 보장하고 데이터를 보낸 순서와 받는 순서를 보장해준다.
- HTTP, FTP, SMTP 등의 프로토콜은 TCP를 기반으로 하고 있으며 이 프로토콜들은 IP 위에서 동작하기 때문에 묶어서 TCP/IP로 부른다.

</br>

- 또한 TCP/IP를 사용한다는 것은 IP 주소 체계를 따르면서 TCP의 특성을 활용해 송신자와 수신자의 논리적 연결을 생성하고 신뢰성을 유지할 수 있도록 하겠다는 의미이다.
- 즉 TCP/IP를 말한다는 것은 송신자가 수신자에게 IP 주소를 사용해 데이터를 전달하고 그 데이터가 제대로 갔는지, 너무 빠르지는 않는지, 제대로 받았다고 연락은 오는지에 대한 이야기를 하고 있는 것이다.

</br>

- 인터넷에서 무언가를 다운로드할 때 중간에 끊기거나 빠지는 부분이 없이 완벽하게 받을 수 있는 이유도 TCP의 이러한 특성 때문이다.
- 그렇기 때문에 HTTP, HTTPS, FTP, SMTP 등과 같이 데이터를 안정적으로 모두 보내는 것을 중요시하는 프로토콜들의 기반이 된다.

### TCP (Transmission Control Protocol)

- `TCP 프로토콜` 은 **OSI 7 Layer에서 4계층인 전송 계층**에 위치한다.
- TCP는 네트워크 정보 전달을 통제하는 프로토콜이자 인터넷을 이루는 핵심 프로토콜 중 하나이다.
- 근거리 통신망이나 인트라넷, 인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 데이터 전송을 안정적으로, 순서대로, 에러 없이 교환할 수 있게 해준다.
- 웹 브라우저들이 www를 통해 서버에 연결할 때 사용되며, 이메일 전송이나 파일 전송에도 사용된다.

</br>

- IP가 패킷들의 관계를 이해하지 못하고 그저 목적지를 제대로 찾아가는 것에 중점을 둔다면 `TCP`는 통신하고자 하는 양쪽 단말이 통신할 준비가 되었는지, 데이터가 제대로 전송되었는지, 데이터가 가는 도중 변질되지는 않았는지, 수신자가 얼마나 받았고 빠진 부분은 없는지 등을 점검한다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/tcp1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 이런 정보들은 `TCP Header`에 담겨 있으며 Source Port, Destination Port, Sequence Number, Window Size, Checksum과 같은 `신뢰성 보장`과 `흐름 제어`, `혼잡 제어`에 관여할 수 있는 요소들도 포함되어 있다.
- 또한 IP Header와 TCP Header를 제외한 TCP가 실을 수 있는 데이터의 크기를 세그먼트(Segment)라고 부른다.

</br>

- TCP는 IP의 정보뿐만 아니라 **Port를 이용하여 연결**한다.
- 힌쪽 단말에 도착한 데이터가 어느 입구(Port)로 들어가야 하는지 알아야 연결을 시도할 수 있기 때문이다.
- 위의 TCP Header를 보면 발신지 포트주소 (Source Port)와 목적지 포트주소 (Destination Port)를 확인 할 수 있다. (예시로, 양쪽 단말에서 HTTP로 이루어진 문서를 주고받고자 할 경우 데이터 통신을 하려면 단말의 Port가 80이어야만 가능합니다.)

### 3-way handshake
- TCP를 사용하는 송신자와 수신자는 데이터를 전송하기 전 먼저 서로 통신이 가능한지 의사를 묻고 한 번에 얼마나 받을 수 있는지 등의 정보를 확인한다.
- 이는 데이터를 안전하고 빠지는 부분 없이 보내기 위한 신뢰성 있는 통신을 하기 위해서이다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/tcp2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- TCP는 TCP Header 내의 SYN, SYN/ACK, ACK Flag를 사용해 통신을 시도한다.
1. 송신자가 수신자에게 SYN를 보내 통신이 가능한지 확인 -> Port는 열려 있어야함
2. 수신자가 송신자로부터 SYN를 받고 SYN/ACK를 송신자에게 보내 통신 준비가 되었다고 함.
3. 송신자가 수신자의 SYN/ACK를 받고 ACK를 날려 전송을 시작함을 알림 </br>
위 과정을 3-way handshake 라고 부른다.

</br>

**TCP로 이루어진 모든 통신은 반드시 3-way handshake를 통해 시작한다.**

- 수신자가 받을 생각이 있는지 준비가 되어있는지 송신자가 보낼 준비가 되어있는지를 미리 확인한 후 통신을 시작해 데이터를 안전하게 보내는 것이다.
- 그리고 데이터를 받았을 때 `ACK`를 송신자에게 보내 데이터가 온전히 도착했음을 알린다.
- 송신자는 `ACK`를 받으면 수신자에게 데이터가 잘 보내졌음을 확인하고 다음 데이터를 전달할 준비를 한다.

### 특징
**1. 흐름제어**

- `송신자`는 자신이 한 번에 얼마를 보낼 수 있는지, 수신자는 자신이 데이터를 어디까지 받았는지 계속 확인하고 TCP Header 내의 Window size를 이용해 한 번에 받고, 보낼 수 있는 데이터의 양을 정한다. (여기서 window 는 일정량의 데이터를 말합니다.)
- `수신자`가 데이터를 받을 Window size를 정하고 (3-way handshake 때 정한다) 자신의 상황에 따라 Window size를 조절한다.
- 그리고 자신이 지금까지 받은 데이터의 양을 확인해 송신자에게 보내는데 이를 `Acknowledgment Number` 라고 한다.
- 만약 수신자가 130번째 데이터를 받았으면, `Acknowledgment Number` 에 1을 더해서 131을 보낸다.
- 이것은 현재 130번까지 받았으니 131번부터 보내면 된다는 의미이다.
- 그리고 이러한 순서 번호를 표기한 것이 `Sequence Number` 이다.

**2. 혼잡제어**

- **데이터가 지나가는 네트워크망의 혼잡을 제어하는 것이다.**
- `Slow Start` 는 연결 초기에 송신자와 수신자가 데이터를 주고받을 준비가 되어있더라도 중간 경로인 네트워크가 혼잡하다면 데이터가 안전하게 전송할지 못할 것에 대비하는 것이다.
- `송신자`는 연결 초기에 데이터 송출량을 낮게 잡고 보내면서 수신자의 수신을 확인해가며 데이터 송출량을 조금씩 늘린다.
- 그러다보면 현재 네트워크에서 가장 적합한 데이터 송출량을 확인할 수 있게 된다.
- 이것이 `Slow Start`이다.

### IP (Internet Protocol)
- `IP 프로토콜` 은 OSI 7 Layer 중 3 계층인 네트워크 계층에 해당한다.
- IP는 TCP와는 달리 **데이터의 재조합이나 손실여부 확인이 불가능**하며, 단지 데이터를 전달하는 역할만을 담당한다.

</br>

- 컴퓨터와 컴퓨터 간에 데이터를 전송하기 위해서는 각 컴퓨터의 주소가 필요하다.
- **IP는 4바이트로 이루어진 컴퓨터 주소이며 3개의 마침표로 나누어진 숫자**로 표시된다.
(예시 `127.0.0.1`)</br>
- IP 주소는 하드웨어 고유의 식별 번호인 MAC 주소와 다르게 임시적으로 다른 주체(대부분 통신사)에게 받는 주소이므로 바뀔 수 있다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

---

### UDP

- `UDP` 는 `User Datagram Protocol` 의 약자로 **OSI 7 Layer에서 4계층인 전송 계층**에 위차한다.
- `TCP` 에 대비되는 프로토콜로 신뢰성이 낮고 완전성을 보장하지 않는다. 하지만 속도가 빠르다는 장점이 있다.

### 특징

- UDP는 **비연결성**이고, **신뢰성이 없으며**, **순서화되지 않은** Datagram 서비스를 제공한다.
- 데이터 전송 단위는 `메세지` 이다. (TCP의 데이터 전송 단위는 세그먼트)

### UDP가 하지 않는 것

- 연결 셋업과 종료 (Connection setup/teardown)
  - TCP의 3-way handshaking과 같은 연결이 필요없는 비연결성 프로토콜이다.
  - 그래서 데이터그램 지향의 전송계층용 프로토콜이라고 많이 부른다.
- 수신 완료했다는 알림 (Acknowledgement)
  - 메세지가 제대로 도착했는지 확인하는 확인응답 작업이 없다.
- 재전송 (Congestion Control)
- 혼잡 제어 (In-order delivery)
  - 흐름 제어를 위한 피드백을 제공하지 않고, 특별한 오류 검출 및 제어가 없어 UDP를 사용하는 프로그램 쪽에서 오류 제어 기능을 스스로 갖춰야 한다.
- 순서대로 보내기
  - 수신된 메시지의 순서를 맞추는 순서제어가 없어 TCP 헤더와 달리 순서번호 필드가 없다.
- Fragmentation


### UDP의 주요 기능
- 실시간 (Real-time)
  - UDP는 빠른 요청과 응답이 필요한 실시간 응용에 적합하다.
  - 제약 조건이 거의 없고 TCP에 비해 매우 빠르기 떄문이다. (인터넷 전화, 스트리밍 등)
- 간단한 트랜잭션 (Simple Transactions)
  - TCP는 Setup과 종료, ACK를 모두 체크해야해 복잡한 transaction이 요구된다.
  - 하지만 UDP는 위의 과정을 체크하지 않기 때문에 transaction이 간단하다. (DNS, DHCP, SNMP 등)
- 멀티캐스트/브로드캐스트
  - TCP는 전송측과 수신측이 서로 확인되어야 데이터를 주고받는다.
  - Point to point 방식으로 동작하는 TCP는 멀티캐스트와 브로드캐스트 전송이 모두 불가능하다.
  - UDP만 가능한 기능이며 전송 속도에 제한이 없다.

### UDP 패킷 헤더 구조

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/udp1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- TCP 헤더에 비해 매우 단순하다.
- **발신/수신 포트번호**가 존재하고 바이트 단위의 길이가 있다.
- **체크섬**은 선택 항목이며 체크섬 값이 0이면 수신측은 체크섬 계산을 하지 않는다.
- 기본적으로 UDP 헤더는 고정 크기의 8 바이트만 사용하며 헤더 처리에 많은 시간이 들지 않는다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

---

### 대칭키-공개키

### 네트워크 보안

- secure communication을 위해서는 다음의 원칙들을 고려해야한다.
1. 기밀성 송신자와 정해진 수신자만이 전송된 메세지의 내용을 이해할 수 있어야한다.
2. 메세지 무결성 송신자와 수신자 사이의 메세지는 중간에 변형되면 안된다.
3. 엔드포인트 인증 발신자와 수신자 모두 통신에 관련된 상대방(End-point)의 신원을 확인할 수 있어야한다.
4. 운영 보안 공격자가 바이러스를 심거나 보안사항을 얻으려는 시도를 하거나, DoS 공격을 시도하는 등을 할 수 없게 안전하게 운영되어야한다.

이 중 대칭키와 비대칭키는 1번 원칙인 기밀성을 위해 사용되는 도구이다. </br>

### 암호화의 원칙

- 다음은 암호화의 요소에 대한 그림이다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/key1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- Alice는 암호화 알고리즘에 input으로 들어갈 key를 제공한다. 이 때, key는 숫자와 문자로 구성된 문자열이다. 이 암호화 알고리즘은 송신자의 키와 plaintext 메세지를 받아서 output으로 암호문을 만들어낸다. 복호화 알고리즘은 암호화 알고리즘을 통해 만들어진 암호문을 수신자의 키를 이용해서 plaintext 메세지로 바꿔준다. 이런 과정에서 사용되는 키는 대칭키와 비대칭키가 있다.

> 대칭키 : 수신자와 송신자의 키가 동일하다. </br>
> 공개키 : 수신자와 송신자의 키가 쌍으로 사용된다.

### 대칭키

**stream 암호**

- plaintext와 같은 길이의 키 스트림을 생성해서 비트단위로 XOR연산을 수행한다. 오류 확산의 위험이 없고, 이동통신 환경에서 구현이 용이해서 무선 데이터 보호에 많이 사용된다. 실시간성이 중요한 음성, 영상, 스트리밍 전송에 사용된다. 비트 단위로 암호화를 진행해서 시간이 많이 걸리고, 데이터 흐름에 따라서 비트 단위로 순차적으로 처리해서 내부 상태를 저장하고 내부 상태를 저장하고 있어야한다는 단점이 있다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/key2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

### RC4
- SSL/TLS나 네트워크 프로토콜에서 자주 사용되는 스트림 암호 기법으로 plaintext와 XOR연산을 진행할 pseudorandom stram을 만든다.
- 256 바이트로 구성된 상태의 한 바이트는 암호화 키로서 사용되기 위해서 랜덤하게 선택이 된다.
- 초기화는 256 바이트의 state vector를 0,1,2,...,254,255로 초기화한다. 초기화 한 후에 키 배열을 이용해서 상태배열에 대해 다음과 같이 swap을 해준다.
  
<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/key3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 이 swap 과정 중 S[i] + S[j]의 값에 해당하는 상태 배열의 인덱스의 원소를 키로 사용한다.

### block 암호

- 다양한 보안이 적용된 인터넷 프로토콜(ex. PGP, SSL, IPsec)에서 사용되는 암호이다. 블록 암호문에서는 암호화될 메세지는 k bit의 블록으로 처리된다. 예를 들면, k = 64인 경우에는 메세지는 64 비트의 블록 단위로 나눠지고, 각각의 블록들은 독립적으로 암호화된다.
- 블록을 암호화 하기위해서는 암호는 일대일 매핑을 사용해서 k비트의 일반 텍스트 블록을 암호문의 k비트 블록에 매핑한다.
- k = 3인 경우 아래와 같이 매핑할 수 있다. 이는 가능한 8!(=40320)가지 방법 중 한가지를 표시한 것이다.

|input|output|input|output|
|---|---|---|---|
000|110|100|011|
001|111|101|010|
010|101|110|000|
011|100|111|001|

- 우리는 이런 각각의 매핑들을 키로 생각할 수 있다. 하지만 이처럼 작은 비트로 매핑을 하면 모든 경우의 수를 완전탐색으로 금방 찾아낼 수 있다. 이런 공격을 방지하기 위해서 k bit를 64비트나 그 이상의 비트수로 구성한다.

- 비록 이런 적절한 k를 이용한 full-table block 암호가 강력한 대칭키 암호 스키마를 만들 수 있지만, 구현하는 것이 까다롭다. k bit를 사용하면 송신자와 수신자 모두 (2^k)!가지의 경우의 수로 구성된 테이블을 유지해야하는데, 이는 실행이 불가능하다. 어찌어찌해서 다 만들었다하더라도, 키를 바꿔버리면 다시 테이블을 생성해야한다.

- 그래서 full-table 암호는 모든 입력과 출력 간에 미리 결정된 mapping을 제공하는 경우에만 사용한다.
- 이런 점을 해결하기 위해서 블록 암호는 랜덤하게 조합된 테이블을 만드는 함수들을 사용한다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/key4.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 위의 그림처럼 input을 다루기 쉬운 사이즈의 bit로 나눠서 매핑한다. 이렇게 나눠진 chunk들은 64비트의 블록으로 합쳐진 후에, 다시 한 번 섞여서 새로운 64-bit output을 만든다. 이렇게 만들어진 결과물은 64-bit input으로 사용되어 위 과정을 반복하고, 이 반복을 총 n번 반복한다. 이 떄, n번의 싸이클을 돌리는 목적은 각각의 input bit가 출력 비트의 대부분에 영향을 미치게하기 위함이다. (chunk 안에 있는 bit는 바뀌는 것이 없기 때문)

### AES

- AES는 128 비트 블록을 사용하고 128, 192, 256 비트 길이의 키를 사용할 수 있다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/key5.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 위 그림은 다음 4가지 단계를 표현한 것이다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/key6.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

1. SubByte : 바이트 단위 형태로 블록을 교환 cf) S-box
2. Shift rows : 행과 행을 치환
3. Mix columns : 열에 속한 모든 바이트를 순환 행렬을 사용해서 함수로 열에 있는 각 바이트를 대체해서 변화시킨다.
4. Add round key : 확장된 키의 일부와 현재 블록을 비트별로 XOR 연산해준다.

- 암호화와 복호화를 위해서 라운드 키 더하기 단계에서 시작해 10라운드를 수행한다. 9라운드 동안은 4단계를 모두 포함하는 반복을 수행한 후에 10번째에는 3단계(mix columns제외)로 구성된 반복을 수행한다.
- 라운드 키를 더하는 단계에서만 키를 사용하기 때문에 각 라운드의 시작과 끝은 라운드 키를 더하는 단계가 된다.
- 위의 4가지 단계는 비트를 뒤섞고 XOR 암호화 하는 것을 번갈아서 적용함으로서 효과적으로 보안성을 강화시킨다.
- 암호화된 암호문은 암호의 역순으로 해독하면 평문을 얻어낼 수 있다.

### 공개키 (Public Key)

- 대칭키를 이용한 암호화 통신은 두 communicating 당사자들이 공통된 키를 공유한다. 이런 방법의 한가지 어려운 점은 두 참가자가 반드시 공유키에 대한 동의를 해야한다는 것이다. 참가자들이 처음 만나서 동의한 다음 그 후에 암호화로 통신이 가능할 것이다. 그러나 지금 세상에는 네트워크 없이 통신의 참여자가 직접 만나거나 소통을 할 수 없다. 그렇다면 두 참여자가 사전에 이미 알고 있는 비밀키 공유 없이 암호호 통신을 할 수 있는 방법은 무엇일까?

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/key7.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 그 때 사용하는 것이 공개키(Public key)이다. 공개키 구조는 네트워크에 참여하는 모두가 볼 수 있는 공개키와 수신자만 가지고 있는 개인키로 되어 있다. 공개키로 암호화되어진 암호문을 수신자의 개인키를 이용해서 복호화한다. 이런 특징 때문에, 공격자가 암호 알고리즘과 암호키를 알아도 복호키 계산이 불가능하다. 공개키를 이용해서 암호화를 할 때, 주로 RS 알고리즘을 이용해서 암호화한다.

RSA는 소인수분해 연산을 이용한다.

1. p와 q라고하는 2개의 서로 다른 충분히 큰 소수를 고릅니다.
2. n = pq, z = (p-1)(q-1)을 계산합니다.
3. n보다 작으면서 서로소인 정수 e를 찾습니다.
4. 그 후 d*e를 z로 나눴을 대 나머지가 1인 정수 d(ed mod z = 1)를 구합니다.
5. (n,e)는 공개키로 사용, (n,d)는 개인키로 사용 이 때, p와q를 이용해서 d,e를 계산하는 것이 가능하기 때문에, 보안상의 이유로 공개키와 개인키를 생성한 이후에는 p와 q를 지워버리는 것이 안전합니다.

- 이 떄, e는 공개키에 이용되고, d는 개인키에 사용된다.

> 암호화 C = (M^e)(mod N) M 은 송신자가 보내는 메세지이고, C는 암호화 값입니다. 이때 C의 비트 패턴은 수신자에게 보내는 암호문과 관련이 있습니다.
> 복호화 M = (C^d)(mod N)

다음은 love라는 단어를 암호화하고 복호화하는 과정을 나타낸 그림입니다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/key8.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 그렇다면 RSA는 어떻게 암호화 알고리즘으로서 역할을 할 수 있을까?

1. c = (m^e) mod n
2. [{(m^e) mod n}^d] mod n = (m^ed) mod n
3. (m^ed) mod n = (m^(ed mod z) mod n) = m mod n = m
4. (((m^d)mod n)^e) mod n = m^de mod n = m^ed mod n = (m^e mod n)^d mod n 위와 같이 (m^d mod n)^e와 (m^e mod n)^d 가 n에 대해서 합동이고, d와 n을 이용해서 e를 구할 수 있기 때문에 암호화 알고리즘으로서의 역할을 할 수 있습니다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

---

### load balancing

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 컴퓨터 네트워크 기술의 일종으로 둘 혹인 셋 이상의 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에 작업을 나누는 것을 의미한다.
- 서버에 가해지는 부하(load)를 분산시켜 balance를 맞춰주는 기술이다.
- **load balancing이 필요한 이유**는 서비스의 규모가 점점 커지고 클라이언트의 수가 늘어나면 기존에 사용하던 서버가 감당할 수 없는 경우 정상적인 서비스가 불가능하다.
- 방법 
1. scale-up : 서버의 하드웨어 성능을 올림
2. scale-down : 서버의 개수를 늘려서 여러대의 서버가 나눠서 작업을 수행 scale-out을 주로 사용한다.

### 종류

- OSI 7계층 기반으로 구분해서 나뉜다. 이 과정에서 DNS에 대한 요청과 응답이 발생한다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- L2 - MAC 주소를 기준으로 분산 작업처리
- L3 - IP 주소를 기반으로 분산 작업 처리

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- L4 Transport Layer (IP & Port) 레벨에서 분산처리(TCP, UDP)
  
<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing4.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- NLB라고도 하며, TCP/UDP를 기준으로 로드밸런싱하는 역할 IP와 포트 정보를 보고 정해진 방식에 따라서 라우팅을해 로드를 분산시킨다. L4로드 밸런서는 TLS/SSL termination의 유무에 따라서 2개의 디자인으로 분류된다.

1. TCP/UDP Termination 로드 밸런서

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing5.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 지연시간이 낮고 TLS Termination을 load balancer가 수행한다.

2. TCP/UDP Passthroungh 로드 밸런서

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing6.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 연결 추적과 NAT을 수행한 뒤에 각 연결에 대한 패킷을 백엔드로 전달한다. TLS termination을 사용하지 않기 때문에 로드밸런서에 가해지는 부하가 적어지기 때문에 훨씬 많은 연결 및 패킷을 처리할 수 있다. 또한, Termination과 다르게 DSR이 가능해진다.

> TLS/SSL termination : TLS/SSL 통신이 끝났음을 통보하는 과정으로 트래픽을 암호화 및 복호화 하는 연산으로 부터 백엔드 서버를 분리시키기 위한 작업이다. ex) http/https 통신

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing7.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- L7 Application Layer(사용자의 Request) 레벨 (IP와 포트번호, 패킷의 URL 정보, 쿠키, payload 등) 정보들을 기준으로 분산처리

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing8.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 하위 레이어의 로드밸런서보다 세부적으로 로드 밸런싱이 가능하다는 것이 특징이다. MSA에서 마이크로 서비스간의 통신은 보통 HTTP를 사용한다. 패킷 내용을 복호화해서 처리하기 때문에 이 과정에서 부하가 많이 발생할 수 있다.

### 주요 기술

### NAT (Network address Translation)

- [Private IP](https://github.com/dltkd1395/CS-study/tree/main/Network#공인-ip-사설-ip)를 [Public IP](https://github.com/dltkd1395/CS-study/tree/main/Network#공인-ip-사설-ip)로 바꾸는데 사용하는 통신망의 주소 변조기로 패킷이 로드밸런서를 통과할 때 패킷의 ip/port 정보를 변경하는 역할을 한다. 

### Tunneling

- 인터넷 상에 보이지않는 통로를 만들어 통신할 수 있게하는 개념. 데이터를 캡슐화해 연결된 노드만 캡슐을 해제할 수 있게 만들어준다.

### DSR(Direction Server Return)

- 로드벨런서 사용시 서버에서 클라이언트로 요청에 대한 응답을 할 때, 로드밸런서(스위치의 IP주소)가 아닌 클라이언트의 IP로 응답을 보내 네트워크 스위치를 거치지않고 클라이언트를 찾아갈 수 있게 해준다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing9.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

### 동작 방식

**Bridge/Transparent Mode**
- 사용자가 서비스를 요청하면 L4로 전달된 목적지 IP 주소를 real server IP 주소로 변조하고 MAC 주소를 변조해서 목적지를 찾아가는 방식
1. 요청 전달 시 변조 사용자 > L4 > NAT(IP/MAC 주소 변조) > real server 사용자가 L4를 호출하면 중간에 NAT가 목적지 IP 주소를 real server IP 주소로 변조하고 MAC 주소도 변조한다. 
2. 응답 전달 시 변조 - real server > NAT > L4 > 사용자 - real server에서 L4를 거치면서 출발지(source) IP 주소를 L4 가상 IP주소로 변조한다. 동일 네트워크 대역이므로 MAC 주소는 변조하지 않는다.

</br>

**Router Mode**
- Bridge/Transparent Mode와 유사하지만 출발지(source) MAC 주소도 변조된다.

</br>

**One Arm Mode**
- 사용자가 real server에 접근할 때 목적지 IP는 L4 스위치 IP를 바라본다. L4에 도달하면 L4가 클라이언트에게 받은 목적지 IP 주소를 L4 IP 주소에서 real server IP와 real server MAC 주소로 변조한다. 되돌아가는 IP는 L4의 IP pool의 IP 주소로 변조한다.

</br>

**DSR(Direct Server Return) Mode**
- 사용자가 real server에 접근할 때 출발지와 목적지의 IP 주소를 변조하지 않고, L4에서 관리하는 real server의 MAC 주소 테이블을 확인해서 MAC 주소만 변조한다.

</br>

**Load Balancing 알고리즘 종류**
- Round Robin : 서버에 들어온 요청을 순서대로 돌아가면서 처리하는 방식으로 서법와 연결이 오래 지속되지 않은 경우 적합하다.
- Weighted Round Robin : 각 서버에 가중치를 매긴 후에 가중치가 높은 서버에 요청을 우선적으로 배정 서버마다 트래픽 처리 능력이 다른 경우에 사용이 권장된다.
- Least Connection : 연결개수가 가장 적은 서버 트래픽으로 인해서 세션이 길어지는 경우에 권장되는 방법
- Weighted Least Connection : Least Connection 방식에 가중치를 적용한 방법으로 서버마다 트래픽 처리 능력이 다른 경우에 사용이 권장된다.
- Fastest Response Time : 서버가 요청에 대해 응답시간을 체크해 가장 빠른 서버로 요청을 분배하는 방식
- Source 사용자 IP를 해싱해서 분배하는 방식 : 특정 사용자가 항상 같은 서버에 접속함을 보장한다.

### 장애대비

- 로드밸런서 이중화 서버를 분해하는 로드 밸런서에 문제가 생길 수 있어서 로드 밸런서를 이중화해서 대비한다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/loadbalancing10.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 이중화된 로드 밸런서들은 서로의 Health Check를 수행한 후에 Main Load Balancer가 동작하지 않으면 VIP (Virtual IP)는 여분의 Load Balancer로 변경하고 이후 여분의 로드밸런서로 운영하도록 하는 방식으로 장애에 대처할 수 있다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

---

### Blocking vs Non Blocking IO 와 Synchronous vs Asynchronous IO

**I/O 작업**

- I/O란 Input/Output의 약자로 입출력 작업을 말한다.
- 네트워크에서는 소켓으로 연결되어 있는 다른 프로세스에게 데이터를 보내는 출력 (`send()`, `write()`) 작업과 다른 프로세스로부터 데이터를 받는 입력 (`rev()`, `read()`) 작업이 수행된다.
- I/O 작업은 유저 프로세스(쓰레드)가 커널에 요청을 하면, 커널 레벨에서 작업을 수행한 뒤 다시 유저 프로세스에게 결과를 반환하는 방식으로 진행된다.

### 봉쇄(Blocking) 모델과 비봉쇄(Non-Blocking) 모델

- 프로그램 유휴 상태를 묘사, 제어권을 묘사
- 봉쇄(Blocking) 방법은 유저 프로세스가 커널에게 입출력 작업 요청을 위한 함수를 호출하면 커널은 작업이 완료될 떄 까지 함수를 반환하지 않는다. 따라서 유저 프로세스는 커널에서 **함수가 반활될 때 까지 프로그램을 동작시키지 않고 대기**한다. **프로세스 제어권은 커널**에게 있다.
- 비봉쇄(Non-Blocking) 방법은 유저 프로세스가 함수를 호출하면 커널은 작업 완료의 여부와 상관없이 함수를 바로 반환한다. 따라서 유저 프로세스는 **대기하지 않고 프로그램을 동작**시킬 수 있다. **프로세스 제어권은 유저 프로세스**에게 있다.

### 동기(Synchronous)와 비동기(Asynchronous)

- 현재 작업에 대한 응답과 다음 작업에 대한 요청 타이밍을 묘사, 데이터 상태에 대한 인지를 묘사
- 현재 작업에 대한 **응답을 받음과 동시에 다음 작업에 대한 요청**을 할 수 있어 **작업의 종료가 순차적**인 방법을 동기(Synchronous), 현재 작업에 대한 **응답을 받지 않아도 다음 작업을 요청**할 수 있어 **작업의 종료가 순차적이지 않은** 방법을 비동기(Asynchronous)라고 한다.

- 동기 방법에서는 **유저 프로세스와 커널이 모두 데이터 상태를 인지**하고 있어야 유저 프로세스가 커널에게 다음 작업을 요청할 수 있다. 따라서 유저 프로세스는 커널 프로세스처럼 데이터 상태를 인지하고 있다. 유저 프로세스는 데이터 상태를 인지하기 위해 커널에게 입출력 작업을 요청한 뒤 **지속적으로 커널에게 작업 완료 여부**를 물어본다.
- 하지만 비동기 방법에서는 유저 프로세스가 현재 작업 완료와 상관없이 다음 작업을 요청할 수 있으므로 **유저 프로세스는 데이터 상태를 인지하고 있지 않아도 된다.**
- 따라서 커널 프로세스가 입출력 작업을 완료했다면 **이벤트 핸들러(Callback 함수 호출)를 동작**시켜 작업 완료 여부를 유저 프로세스에게 통지함으로써 유저 프로세스는 작업의 종료 여부를 알 수 있다.
- 봉쇄/비봉쇄, 동기/비동기 방식은 동일한 개념이 아니기 때문에 혼잡되어 사용될 수 있음을 주의하자!

### Synchronous Blocking I/O

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/synchronous1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 가장 기본적인 I/O 모델
- 유저 프로세스가 `read()` 함수를 호출하면 커널은 버퍼에 데이터가 복사되기 전까지 read() **함수를 반환하지 않는다.** 함수가 반환되지 않는 동안 프로세스는 **봉쇄되어 대기하고 있으며 다른 프로세스를 진행할 수 없다.** 데이터가 입력되면 커널은 프로세스에게 `read()` 함수를 반환되어 데이터가 복사된다.

### Synchronous Non-Blocking I/O

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/synchronous2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 유저 프로세스가 `read()` 함수를 호출하면 커널은 데이터 **복사 여부와 무관하게 `read()` 함수를 반환**한다. 만약 아직 데이터가 복사되지 않은 상태라면 에러 코드를 반환한다. 이 과정은 버퍼에 데이터가 복사될 떄 까지 반복된다. 유저 프로세스가 함수를 호출해도 바로 반환되므로 **다른 프로세스를 동시에 작업할 수 있다.**
- 또한, 유저 프로세스는 지속적으로 시스템 콜을 호출하며 데이터 상태를 인지하고 있다. 비로소 데이터 입출력 작업이 완료되었다면 커널은 에러 코드를 반환하는 대신 데이터를 복사한 결과를 반환한다.

- `Synchronous Blocking I/O 모델`과 달리 여러 프로세스를 동시에 작업할 수 있다는 장점이 있지만, 데이터가 준비되기 전에는 유저 프로세스와 커널이 바쁘게 순환해야한다(busy wait)는 단점이 있다.

### Asynchronous Blocking I/O

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/synchronous3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- `Synchronous Non-Blocking I/O 모델`의 busy wait 문제를 해결할 수 있는 모델

### IBM 문서에 의한 설명

- 입출력 함수(`read()`)를 호출하기 전, 커널에 입출력 데이터가 들어왔는지 여부를 확인하는 함수인 `select()`를 호출한다. 만약 **커널에 들어온 입출력 데이터가 없다면 유저 프로세스는 봉쇄**된다. 입출력 데이터가 있다면 유저 프로세스는 입출력 함수를 호출할 수 있다.
- 하지만 위의 설명을 뜯어보면 유저 프로세스가 `select()`를 호출하여, 입출력 데이터가 있는지를 유저 프로세스가 획인하고 있다. 따라서 동기 방식으로 볼 수 있다는 논란의 여지가 있다.

### 비동기 Select

- `WSAEventSelect` 소켓 통지 모델을 사용한다면 유저 프로세스가 지속적으로 커널의 데이터 상태를 확인할 필요 없이, 기존 상태와 비교하여 데이터 상태가 달라지면 **이벤트 핸들러를 통해 콜백 함수가 호출**된다. 따라서 비동기 방식으로 `select()` 기능을 사용할 수 있다.

### Asynchronous Non-Blocking I/O

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/synchronous3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">


- 유저 프로세스가 입출력 함수를 호출하면 커널은 데이터 상태와 무관하게 바로 함수를 반환한다. 유저 프로세스는 **커널의 데이터 상태에 제약 없이 다른 프로세스를 작업**할 수 있다. 또한 유저 프로세스는 데이터 입출력 여부를 물어보기 위해 지속적으로 커널에 함수를 호출할 필요가 없다. 데이터가 준비되면 커널이 **이벤트 핸들러를 통해 콜백 함수를 호출**하여 결과를 통지한다.

### 정리

> Blocking : 유저 프로세스가 입출력 작업을 위한 함수를 호출하면, 커널은 작업이 완료될 때까지 함수를 반환하지 않아 현재 프로세스가 봉쇄된다. </br>
> Non-Blocking : 유저 프로세스가 입출력 작업을 위한 함수를 호출하면, 커널은 작업 종료 여부와 무관하게 함수를 바로 반환한다. 따라서 현재 프로세스가 봉쇄되지 않아 여러 작업을 수행할 수 있다. </br>
> Synchronous : 작업 요청을 보낸 유저 프로세스가 작업 완료 여부를 확인한다. </br>
> Asynchronous : 작업 요청을 받은 커널이 작업 완료 여부를 통지한다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

--

### 웹 동작 방식

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/web1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">


1, 2. 사용자가 웹 브라우저에 웹 페이지의 URL 주소를 입력한다. </br>
3. 웹 브라이줘는 URL 주소 중에서 도메인 네임(domain name) 부분을 DNS 서버에서 검색한다.
4. DNS 서버에서 해당 도메인 네임에 해당하는 IP 주소를 찾고 사용자가 입력한 URL 정보와 함께 전달한다.
5. IP 주소와 URL 정보는 HTTP 프로토콜을 사용하여 HTTP 요청 메시지(HTTP Request)를 생성한다.
6. 이렇게 생성된 HTTP 요청 메시지는 TCP 프로토콜을 사용하여 인터넷을 거쳐 해당 IP 주소의 컴퓨터로 전송된다.
7. 도착한 HTTP 요청 메시지는 HTTP 프로토콜을 사용하여 웹 페이지 URL 정보로 변환된다.
8. 웹 서버는 도착한 웹 페이지 URL 정보에 해당하는 데이터를 검색한다.
9. 검색된 웹 페이지 데이터는 또다시 HTTP 프로토콜을 사용하여 HTTP 응답 메시지(HTTP Response)를 생성한다.
10. 이렇게 생성된 HTTP 응답 메시지는 TCP 프로토콜을 사용하여 인터넷을 거쳐 원래 컴퓨터로 전송된다.
11. 도착한 HTTP 웅답 메시지는 HTTP 프로토콜을 사용하여 웹 페이지 데이터로 변환된다.
12. 웹 브라우저는 변환된 웹 페이지 데이터를 출력한다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

### DNS

### Domain Name System 이란?

- IP 주소는 IPv4 기준 12개 숫자와 '.'으로 구성되어 있어 외우기가 힘들다. 이를 좀 더 알아보기 쉽게 'naver.com', 'google.com'과 같이 문자와 .으로 표현한 주소를 도메인 이름(Domain Name)이라고 한다.
- 네트워크에서 이러한 도메인 이름을 숫자로 된 IP 주소로 변환해주는 TCP/IP 서비스를 DNS라 하며 계층 구조를 가지는 분산데이터베이스 구조이다.

> Hostname은 네트워크에 연결된 장치들에게 부여되는 각각의 고유한 이름 </br>
> ex) naver.com 이라는 Domain Name 내에서 news, comic, mail 등의 Hostname을 이용해 서비스로 구분한다. </br>
> -> news.naver.com, comic.naver.com, mail.naver.com

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/dns1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

### DNS 동작 원리

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/dns2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

1. 도메인을 먼저 Local DNS 서버에 "www.naver.com" query
2. Local DNS 서버에 정보가 없다면 Root DNS 서버에 "www.naver.com" query
3. Root DNS 서버(Root Name Server)에서 "com 도메인"을 관리하는 TLD Name 서버 정보 전달
4. TLD Name 서버에 "www.naver.com" query
5. TLD Name 서버에서 "naver.com" 관리하는 DNS 정보 전달
6. "naver.com" 도메인을 관리하는 DNS 서버에 "www.naver.com"에 대한 IP 주소 query
7. Local DNS 서버에게 222.122.195.6 응답
8. Local DNS는 www.naver.com에 대한 IP 주소를 캐싱하고 IP 주소 정보 전달


### DNS Server

**Local DNS Server (Recursive DNS Server)**
- 사용자가 가장 먼저 접근하는 DNS 서버, DNS 쿼리를 통해 얻은 데이터를 일정 기간 캐시로 저장해둔다. 일반적으로 KT, LG, SK 등의 ISP DNS 서버를 사용한다.

**Root Name Server (Root DNS Server)**
- 국제인터넷주소관리기구(ICANN)에서 직접 관리하는 서버로 인터넷상의 모든 TLD DNS 서버 IP 주소를 저장해두고 전 세계에 13개 만이 존재한다.

**Root DNS Mirror Server**
- 기존 루트 DNS 서버를 복사한 것으로 미러 서버가 있는 국가는 외국의 루트 서버 없이 자체적으로 인터넷 통신을 관리할 수 있다.

**TLD Name Server (Top-Level-Domain DNS Server**
- ICANN의 지사인 인터넷 할당 번호 관리기관(IANA)에서 관리하는 서버로 Authoritative Name Server의 주소를 저장해둔다.

**Authoritative Name Server (Authoritative DNS Server)**
- 실제 도메인과 IP 주소를 매칭한 정보가 저장/변경되는 서버로 보통 가비아, 후이즈와 같은 도메인/호스팅 업체의 네임서버를 의미한다. 개인 DNS 서버를 구축한 경우에도 여기에 해당한다.

#### DNS Query 방버

1. **반복적 질의 (Iterative Query)**

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/dns3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 사용자가 Local DNS 서버에 query를 보내면 Local DNS 서버에 Root name 서버에 query를 보내 TLD 서버의 주소를 반환받고, 다시 TLD 서버에 query를 보낸다. 이렇게 최종 IP 주소를 받을 때 까지 요청과 응답을 계속해서 Local DNS 서버가 반복하는 방법이다.

2. **재귀적 질의(Recursive Query)**

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/dns4.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- 사용자가 Local DNS 서버에 query를 보내면 Local DNS server가 Root name 서버에 query를 보내고, Root 서버는 자신의 서버에 없으면 해당 TLD 서버에 요청한다. 이렇게 재귀적으로 실제 도메인 정보를 가지고 있는 서버까지 query가 이동하여 IP 주소를 얻는 방법이다. 재귀적인 방법은 Root 서버에 너무 큰 부담을 준다는 단점이 있다.

<br>

- 실제 DNS 서버는 반복과 재귀적인 방식을 함께 사용하여 Local DNS 서버에 재귀, Root와 TLD 서버에는 반복, Authoritative 서버에는 재귀/반복적 query를 사용한다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

---

### HTTP 프로토콜

### HTTP란?

- HTTP(Hypertext Transfer Protocol)는 인터넷 상에서 데이터를 주고 받기 위한 `서버/클라이언트 모델`을 따르는 프로토콜이다.
- 애플리케이션(응용) 레벨의 프로토콜로 `TCP/IP`위에서 작동한다.
- HTTP로 보낼 수 있는 데이터는 HTML문서, 이미지, 동영상, 오디오, 텍스트 문서 등 여러 종류가 있다.
- "하이퍼텍스트 기반으로(Hypertext) 데이터를 전송하겠다(Transfer)" = "**링크 기반**으로 데이터에 접속하겠다"는 의미이다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/http1.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

### HTTP 작동방식

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/http2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- HTTP는 기본적으로 요청/응답 **(request/response)** 구조로 되어 있다.
- 클라이언트가 **HTTP Request**를 서버에 보내면 서버는 **HTTP Response**를 보내는 구조.
- 클라이언트와 서버의 모든 통신이 **요청과 응답**으로 이루어진다.


### HTTP의 특징

**비연결성 (Connectionless)**
- 클라이언트에서 서버에 요청을 하고 서버가 요청을 받아 응답하게 되면 **연결을 끊어버리는 특징**
  - 지속적인 연결로 인한 서버 부담이 줄어드는 장점이 있으나 클라이언트의 이전 상태를 알 수가 없게 된다.
  - 이전 상태 정보를 알 수 없게 되면 로그인을 성공하더라도 로그 정보를 유지할 수 없게 된다.

- HTTP 1.1 부턴 **지속적 연결 상태가 기본**이며 이를 해제하기 위해선 명시적으로 요청 헤더를 수정해야 한다.

(참고 Keep-Alive)
- HTTP 프로토콜의 Keep-Alive는 Http의 Header의 일종으로, **HTTP/1.0에서 지원하지 않던 지속 커넥션을 가능하게 하기 위해서**사용되었다.

[HTTP 요청시]

```
Connection: Keep-Alive
```

[HTTP 응답시]

```
Connection: Keep-Alive
Keep-Alive: max=5, timeout=120 
```

Keep-Alive 헤더를 추가적으로 보낼 수 있다.
- Keep-Alive의 max 파라미터는 커넥션이 몇 개의 HTTP 트랜잭션을 처리할 떄까지 유자될 것인지를 의미한다.
- timeout 파라미터는 커넥션이 얼마동안 유지될 것인가를 나타내고, 위의 예시에서는 2분동안 커넥션을 유지하라는 내용이다.


**무상태성 (Stateless)**
- 비연결성 (Connectionless)에서 파생되는 특징으로 **각각의 요청이 독립적으로 여겨지게 되는 특징**
  - 서버는 클라이언트의 상태(State)를 유지하지 않으므로 **Cookie, Session** 등을 이용하여 클라이언트 인증, 인식을 한다.

> Cookie(쿠키) : 서버에 저장하지 않고 클라이언트에 저장되는 방식으로, 개별 클라이언트 상태정보를 HTTP 헤더에 담아 전달하는 데이터 </br>
> Session(세션) : 쿠키와 반대로 클라이언트에 저장되는 것이 아니라 서버에 데이터를 저장하는 방법

### URI

- URI는 HTTP와는 독ㄱ립된 다른 체계다.
- HTTP는 **전송 프로토콜**이고, URI는 **자원의 위치를 알려주기 위한 프로토콜**이다.
- Uniform Resource Identifiers(URL)의 줄임으로, World Wide Web(wwww)상에서 접근하고자 하는 자원의 위치를 나타내기 위해서 사용한다.
- 자원은 HTML 문서, 이미지, 동영상, 오디오, 텍스트 문서등 모든 것이 될 수 있다.

</br>

- 웹페이지의 위치를 나타내기 위해서 사요하는 https://www.naver.com/index.html 등이 URI의 예다.

```
https : 자원에 접근하기 위해서 https 프로토콜을 사용한다.

www.naver.com : 자원의 인터넷 상에서의 위치는 www.naver.com 이다. 
                도메인은 ip 주소로 변환되므로, ip 주소로 서버의 위치를 찾을 수 있다.

index.html : 요청할 자원의 이름이다.
```

- 이렇게 **"프로토콜, "위치", "자원명"**으로 어디에 있던지 자원에 접근할 수 있다.

### HTTP Request(요청) 구조

- HTTP Request 메세지는 크게 3부분으로 구성된다.

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/http3.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- Start Line (Status Line)
- Headers
- Body
</br> </br>

**Start Line (Status Line)**

- 말그대로 HTTP request의 첫라인으로, start line 또한 3부분으로 구성되어 있다.

```http
GET /search HTTP/1.1
```

1. HTTP Method
    - 해당 request가 의도한 action을 정의하는 부분
    - HTTP Methods에는 GET, POST, PUT, DELETE, OPTIONS 등이 있다.
    - 주로 GET과 POST가 쓰인다.

2. Request target
    - 해당 request가 전송되는 **목표 URL**

3. HTTP Version
    - 말 그대로 사용되는 HTTP 버전으로, 1.0, 1.1, 2.0 등이 있다.


**Headers**

- 해당 request에 대한 **추가 정보**를 담고 있는 부분
  - 예를 들어, request 메세지 body의 총 길이 (Content-Length) 등
- Key: **Value** 값으로 되어 있다. (: 이 사용됨)
  - `HOST: google.com` => Key = HOST, Value = google.com

```http
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Type: application/json
Content-Length: 257
Host: google.com
User-Agent: HTTPie/0.9.3
```

- Host : 요청이 전송되는 target의 host url (예를 들어, google.com)
- User-Agent : 요청을 보내는 클라이언트의 대한 정보 (예를 들어, 웹브라우저에 대한 정보)
- Accept : 해당 요청이 받을 수 있는 응답(response) 타입
- Connection : 해당 요청이 끝난 후에 클라이언트와 서버가 계속해서 네트워크 컨넥션을 유지할 것인지 아니면 끊을 것인지에 대해 지시하는 부분
- Content-Type : 해당 요청이 보내느 메세지 body의 타입 (예를 들어, JSON을 보내면 application/json)
- Content-Length : 메세지 body의 길이

**Body**

- 해당 requst의 실제 메세지/내용으로, Body가 없는 request도 많다.
- 예를 들어, GET request들은 대부분 body가 없는 경우가 많음

```http
POST /payment-sync HTTP/1.1
Accept: application/json
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 83
Content-Type: application/json
Host: intropython.com
User-Agent: HTTPie/0.9.3

{
    "imp_uid": "imp_1234567890",
    "merchant_uid": "order_id_8237352",
    "status": "paid"
}
```

### HTTP Response(응답) 구조

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/http4.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

- Start line (Status line)
- Headers
- Body

**Start Line (Status Line)**
- Response의 상태를 간략하게 나타내주는 부분으로, 3부분으로 구성되어 있다.

```http
HTTP/1.1 404 Not Found
```
1. HTTP 버전
2. Status code : 응답 상태를 나타내는 코드 (예를 들어, 200)
3. Status text : 응답 상태를 간략하게 설명해주는 부분 (예를 들어, "Not Found")


**Headers**
- Request의 headers와 동일하다.
- 다만 response에서만 사용되는 header 값들이 있다.
  - 예를 들어, User-Agent 대신에 Server 헤더가 사용된다.

**Body**
- Request의 body와 일반적으로 동일하다.
- Request와 마찬가지로 모든 request가 body가 있지는 않다. 데이터를 전송할 필요가 없을 경우 body가 비어있게 된다.

```http
HTTP/1.1 200 OK
Date: Sat, 17 Oct 2020 07:32:39 GMT
Content-Type: application/json
Content-Length: 332
Connection: close
Server: gunicorn/19.9.0
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true

{
  "args": {}, 
  "data": "Hello", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Content-Length": "5", 
    "Content-Type": "text/plain", 
    "Host": "httpbin.org", 
    "X-Amzn-Trace-Id": "Root=1-5f8a9e17-1755758a691e5b0051977312"
  }, 
  "json": null, 
  "origin": "121.131.70.240", 
  "url": "https://httpbin.org/post"
}
```

### HTML 버전

- 현재는 주로 HTML/1.1, HTML/2.0을 사용한다.

1. HTTP/1.0
 - 처음으로 널리 사용하기 시작한 버전이다.
2. HTTP/1.0+
 - keep alive 커넥션, 프락시 연결 지원 등의 기능이 추가 되었다.
3. HTTP/1.1
 - 1.0에서는 연결하고 끊고를 반복하면 서버나 클라이언트 모두에 부담이 된다. 그래서 1.1은 pipeline (파이프라인) 기능을 추가하여 매전 연결을 맺고 끊고 하는 과정을 줄여서 속도를 높였다.
 - PUT, DELETE 등의 새로운 Method가 추가 되었다.
4. SPDY
-  구글이 만든 프로토콜로, HTTP의 속도를 개선시키기 위해 만들었다.
-  대표적인 기능으로 헤더를 압축하는 기능과 하나의 TCP커넥션에 여러 요청을 동시에 보내는 기능, 클라이언트가 요청을 보내지 않아도 서버가 리소스를 푸시하는 기능 등을 갖추고 있다.
5. HTTP/2.0
- 2012년 구글이 만든 SPDY 프로토콜을 기반으로 만들어진 프로토콜이다.
- 1.1은 커넥션 하나에서 여러개의 파일을 전송할 수 있는 1개의 파이프라인을 연결하는데 2.0은 연결이 되면 여러개의 파이프라인을 꽂는다고 생각하면 된다.
- 이걸 **stream(스트림)**이라고 하는데 1번 파이프라인으로 전송되던 파일이 늦어지면 2번, 3번 또는 다른 파이프라인으로 보내기 때문에 **늦어지는 현상이 1.1에 비해서 짧다는 장점**이 있다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

---

### HTTP와 HTTPS

### HTTP(Hyper Text Transfer Protocol)

- WWW(World-Wide-Web)기반 서비스에서 웹 서버와 WWW 클라이언트(웹 브라우저)간 통신을 위해 사용하는 네트워크 프로토콜
- 일반적으로 `80`번 포트를 사용한다. 클라이언트가 `80`번 포트를 이용해 데이터를 요청(Request)하면 웹 서버는 `80`번 포트로 들어온 요청에 **응답**(Response)하는 방식으로 통신한다.
- HTTP 요청(Request) 메시지와 응답(Response) 메시지는 크게 Start line, Headers, Body 부분으로 구성되어 있다.

> - Start line : Method 방식, 타켓 URL, HTTP 버전 등의 정보 </br>
> - Headers : Request와 Response 메시지 메타 정보 </br>
> - Body : 실제 Request와 및 Response 메시지 내용

- HTTP는 **직관적**이다. 요청 및 응답 메시지(HTML 파일, 텍스트 데이터, 이미지 및 파일 데이터 등)를 **Body에 평문으로 붙여** 전달한다. 따라서 데이터를 **빠르고 쉽게** 주고 받을 수 있다.

### HTTPS(Hyper Text Transfer Protocol over Secure-Soket-Layer)

- HTTP 프로톨에 대해 `SSL 암호화 통신 기능`을 추가한 네트워크 프로토콜
- HTTP는 웹 서버와 클라이언트(브라우저) 간 통신을 제약없이 자유롭게 진행했다면, HTTPS는 웹 서버와 클라이언트(브라우저) 간 통신이 암호화드므로 제 3자의 개입아니 위, 변조를 막을 수 있다.
- 일반적으로 443번 포트를 사용한다. 또한 URL이 `http://`로 시작하는 HTTP 프로토콜과 달리, HTTPS 프로토콜은 `https://`로 시작하므로 URL을 확인하면 어떤 웹 사이트에서 HTTPS 프로토콜을 사용하는지 알 수 있다.


### SSL(Secure Socket Layer)

- 웹 서버와 클라이언트 간 통신을 공인된 제 3자 인증 기관 CA(Certificate Authority)에서 인증하여 보안을 강화하는 방법
  - SSL은 OSI 7계층의 `응용 계층`과 `표현 계층` 중간에 독립적으로 존재한다. 응용 계층이 SSL로 데이터를 전송하면 SSL은 이를 암호화하여 TCP로 보낸 뒤 이것이 외부 인터넷으로 전달된다. 수신 역시 TCP로부터 데이터를 수신받은 SSL은 이를 복호화하여 응용 계층으로 전달한다.
  - 전송 계층 보안(Transprot Layer Security, TLS)은 조금 더 진화된 버전의 SSL이다. 오늘날 대부분 TLS 방식을 이용하지만 SSL이 더많이 알려져 있기 때문에 실제로는 TLS를 쓰고 용어만 SSL이라고 한다.

**공개키 암호화 방식**
- 데이터를 암호화(Excrypt)하고 암호화된 데이터를 다시 평문으로 원상복구하는 복호화(Decrypt) 과정에서 각각 서로 다른 키(Key)를 사용한다.
- A키를 이용해 암호화한 데이터는 B키가 있어야 복호화하여 해석할 수 있다. 두 키는 쌍을 이룬다.
- 암호화 키(공개키)는 모두에게 공개되어 있기 때문에 누구나 암호화할 수 있다.
- 다만 복호화 키(비밀키)는 해당 데이터를 열람하고 수정할 권한이 있는 호스트만 각자 개인의 비밀키를 갖고 있다. 따라서 권한이 있는 자만 데이터를 읽을 수 있다.

**공개키 암호화의 특성을 이용한 전자 서명**
- 위의 공개키 암호화 방식을 응용하여 **정보를 제공한 자의 신원을 보장**할 수 있는 방법이 있다.
  - 비밀키 소유가 자신의 비밀키를 이용해 데이터를 암호화하고, 이 데이터를 공개키와 함께 배포한다.
  - 데이터를 수신한 자는 함께 수신한 공개키를 이용해 데이터를 복호화하여 접근할 수 있다.
- 기존의 공개키 암호화 방식에는 공개키로 암호화한 뒤 비밀키로 복호화했다면 전자 서명에서는 반대로 비밀키로 암호화한 뒤 공개키로 복호화한다. 이 방법은 언뜻보면 누구나 공개키를 이용해 데이ㅇ터를 읽어 위,변조할 수 있어 위험해 보인다. 하지만 암호화된 데이터를 특정 공개키로 복호화할 수 있다는 것은 **해당 데이터가 특정 공개키와 쌍을 이루는 특정 비밀키로 암호화되어 있다**는 것을 의미한다. 따라서 데이터를 제공한 자의 신원을 보장할 수 있다.

**SSL을 이용한 통신 과정**

1. Handshake
   1.  클라이언트가 서버에 접속한다.
       - 전송하는 정보 : 클라이언트가 생성한 랜덤 데이터, 암호화 방식 협상을 위한 제안, 세션 아이디
       - 랜덤 데이터는 실질적인 요청 및 응답 메시지 암호화, 복호화를 위해 사용됨
       - 클라이언트 측에서 가능한 암호화 방식의 종류를 서버 측에 제시
       - 이후 같은 세션에서는 SSL 핸드 쉐이킹을 생략하기 위해 세션 식별자를 함께 보냄 
   2.  서버는 클라이언트의 요청에 응답한다.
       - 전송하는 정보 : 서버가 생성한 랜덤 데이터, 클라이언트의 암호화 방식 중 서버가 선택한 암호화 방식 명시, 인증서
       - 랜덤 데이터는 실질적인 요청 및 응답 메시지 암호화, 복호화를 위해 사용됨
       - 클라이언트가 제시한 암호화 방식 중 가능한 암호화 방식을 선택함
       - 서버가 자기 자신임을 인증하기 위한 인증서 
   3.  클라이언트는 서버의 인증서를 통해 서버의 신원을 판별한다.
       - 클라이언트는 서버의 인증서가 신뢰할 수 있는 CS에서 인증된 것인지 확인한다.
       - 신뢰할 수 있다면 해당 CA의 공개키로 서버의 인증서를 복호화한다.
       - 복호화가 성공했다는 것은 cA의 공개키와 쌍을 이룬 해당 CA의 비밀키로 암호화가 되었다는 것을 의미하므로 서버의 신원을 확실하게 믿을 수 있다.
   4.  실제 HTTPS 통신 메시지를 암호화하기 위해 클라이언트와 서버의 랜덤 메시지를 조합하여 pre master secret 키를 생성한다.
       - pre master secret 키는 대칭키이므로 이를 주고받기 위해 다시 공개키 방식을 이용한다. 서버의 공개키로 pre master secret 키를 암호화하여 보내면 클라이언트는 이를 자신의 비밀키로 복호화하여 메시지를 읽을 키(session key)를 획득한다.
2. 세션
   - 클라이언트와 서버가 실제 데이터를 주고 받는다.
   - handshake 단계에서 공유한 session key(대칭키)를 이용해 메시지를 암호화 및 복호화한다.
   - 대칭키와 공개키를 혼용하는 이유 : 공개키 방식이 상대적으로 많은 연산을 필요로하기 때문에 연산을 최소화하기 위해 실제 데이터에 접근하기 위한 대칭키만 공개키로 암호화하는 것 
3. 세션 종료
   - SSL 통신이 끝났음을 서로에게 통지한다.
   - session key는 폐기한다. 


### HTTP vs HTTPS

1. HTTPS 프로토콜과 HTTP 프로토콜의 가장 큰 차이는 `보안`이다.
   - HTTPS 프로토콜은 SSL 암호화 방식을 이용해 **요청과 응답 주체**를 인증할 수 있고, 전송하는 데이터도 **암호화** 되어있으므로 해독하여 위, 변조할 수 없다. 즉, **데이터의 무결성을 보장**한다. 
   - 사용자의 개인정보나 결제 정보 등과 같이 민감하고 중요한 정보를 전송해야할 경우 HTTPS 프로토콜을 이용해야 ㄴ한다.
2. 부가적인 차이는 `SEO 품질`이다.
    - SEO(Search Engine Optimization, 검색 엔진 최적화) : 구글 등의 검쌕 엔진에서 웹사이트가 잘 검색되고 노출될 수 있도록 검색을 최적화 하는 전략
    - 검색 엔진 구글은 HTTPS 프로토콜을 이용하는 웹 사이트에 대해 SEO 가산점을 제공하여 웹 사이트들이 HTTPS 프로토콜을 이용하도록 유도하고 있다.
    - 나아가 크롬과 같은 브라우저에서는 HTTP 프로토콜을 이용하거나 신뢰할 수 없는 인증서를 이용해 통신할 경우 `안전하지 않음`이라는 메시지를 출력함으로써 사용자가 HTTP 웹 사이트를 접속하는 것을 간접적으로 막고 있다.
    - 또한 구글에서 지원하느 AMP(Accelerated Mobile Pages, 가속화된 모바일 페이지) 혜택을 받기 위해서도 HTTPS 프로토콜을 사용해야 한다.
3. 미묘한 성능 차이가 존재할 수 있으나 기술의 발달로 체감할 수 없는 수준이 되거나 오히려 HTTPS가 더 좋은 성능을 보이기도 하므로 문제가 엇는 수준이다.

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)
