# Network
1. [OSI 7계층](https://github.com/dltkd1395/CS-study/tree/main/Network#osi-7계층)
2. [IP](https://github.com/dltkd1395/CS-study/tree/main/Network#ip)
    1. [IPv4](https://github.com/dltkd1395/CS-study/tree/main/Network#ipv4)
    2. [IPv6](https://github.com/dltkd1395/CS-study/tree/main/Network#ipv6)
    3. [공인 IP, 사설 IP](https://github.com/dltkd1395/CS-study/tree/main/Network#공인-ip-사설-ip)
3. [TCP/IP](https://github.com/dltkd1395/CS-study/tree/main/Network#tcpip)
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

- IPv6의 각 필드의 역할은 다음과 같드

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
- 공인 IP 주소가 외붕 공개되어 있기 때문에 인터넷에 연결된 다른 PC로부터의 접근이 가능하다. 따라서 공인 IP주소를 사용하는 경우에는 방화벽이나 보안 프로그램을 설치할 필요가 있다.

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

| 공인 IP | 사설 IP
|---|---|---|
할당 주체 | ISP(인터넷 서비스 공급자) | 라우터(공유기)
할당 대상 | 개인 또는 회사의 서버(라우터) | 개인 또는 회사의 기기
고유성 | 인터넷 상에서 유일한 주소 | 하나의 네트워크 안에서 유일
공개 여부 | 내/외부 접근 가능 | 외부 접근 불가능

### NAT 
- Network Address Translation의 약자로 OSI 3계층인 네트워크 계층에서 공인 IP와 사설 IP로 변환하는 역을 한다.
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

(공인 IP -> 사설 IP)
3. NAT Binding Table을 참조해서 공인 IP 주소를 사설 IP 주소로 변환해서 단말로 전송한다.

### 고정 IP
- 컴퓨터에 고정적으로 부여된 IP
- 한번 부여되면 반납하기 전까지 다른 장비에 부여할 수 없는 IP 주소
- 인터넷에서 서버를 운영하고자 할 때는 공인 IP를 고정 IP로 부여해야 한다. 공인 IP를 부여받지 못하면 다른 사람이 내 서버에 접속할 수 없고, 고정 IP를 부여하지 않으면  내 서버가 아닌 다른 살마의 서버로 접속할 수 있다.

### 유동 IP
- 장비에 고정적으로 IP를 부여하지 않고 컴퓨터를 사용할 때 남아 있는 IP 중에서 돌아가면서 부여하는 IP

[맨위로](https://github.com/dltkd1395/CS-study/tree/main/Network#network)

### TCP/IP

- `TCP/IP` 는 하나의 트로토콜이 아닌 TCP 프로토콜과 IP 프로토콜을 합쳐서 부르는 말이다.
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

<img src="https://github.com/dltkd1395/CS-study/blob/main/Network/image/tcp2.png" style="max-width: 100%; display: inline-block;" data-target="animated-image.

- TCP는 TCP Header 내의 SYN, SYN/ACK, ACK Flag를 사용해 통신을 시도한다.
1. 송신자가 수신자에게 SYN를 보내 통신이 가능한지 확인 -> Port는 열려 있어야함
2. 수신자가 송신자로부터 SYN를 받고 SYN/ACK를 송신자에게 보내 통신 준비가 되었다고 함.
3. 송신자가 수신자의 SYN/ACK를 받고 ACK를 날려 전송을 시작함을 알림
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
- 그리고 자신이 지금까지 받은 데이터의 양을 확인해 송신자에게 보내는데 이를 `Acknowledment Number` 라고 한다.
- 만약 수신자가 130번째 데이터를 받았으면, `Acknowledment Number` 에 1을 더해서 131을 보낸다.
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