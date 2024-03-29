# TCP/IP

**4계층 응용계층 (Application Layer)**

- OSI 7 Layer에서 세션 계층 , 프레젠테이션 계층, 애플리케이션 계층에 해당합니다. (5, 6, 7 계층)
- 응용프로그램들이 데이터를 처음 받고, 다른 계층의 서비스에 접근할 수 있게 하는 애플리케이션을 제공합니다.
- TCP/UDP 기반의 응용 프로그램을 구분할 때 사용합니다.
- 프로토콜에는 HTTP, SSH 등이 있습니다.

**3 계층 전송 계층 (Transport Layer)**

- OSI 7 Layer에서 전송계층에 해당합니다.
- 통신 노드 간의 연결을 제어하고 신뢰성 있는 전송 기능을 제공합니다.
- 정확한 패킷의 전송을 보장하는 TCP와 정확한 전송을 보장하지 않는 UDP 프로토콜을 이용합니다. 정확한 전송보다 빠른 속도의 전송이 필요한 멀티미디어 통신에서는 TCP 보다 UDP가 좋은 선택일 수 있죠.
- 프로토콜에는 TCP, UDP 등이 있습니다.

**2 계층 인터넷 계층 (Internet Layer)**

- OSI 7 Layer의 네트워크 계층에 해당합니다.
- 인터넷 계층의 주요 기능은 상위 전송계층으로부터 받은 데이터에 IP 패킷 헤더를 붙여 IP 패킷을 만들고 이를 전송하는 역할을 합니다. 또한 통신 노드 간의 IP 패킷을 전송하는 기능 및 라우팅 기능을 담당합니다.
- 프로토콜에는 IP, ARP, RARP 등이 있습니다.

**1 계층 네트워크 액세스 계층 (Network Access Layer)**

- OSI 7 Layer에서 물리계층과 데이터링크 계층에 해당합니다.
- TCP/IP 패킷을 네트워크로 전달, 또는 반대로 네트워크에서 TCP/IP를 받아오는 역할을 합니다. 논리적 주소인 IP가 아니라 물리적 주소인 MAC 주소를 사용하고, 패킷을 프레임으로 변환시켜 최정 적으로 데이터 전송을 하게 되죠.
- 수신 측 컴퓨터의 경우 네트워크 액세스 계층 속 데이터 링크 계층에서 추가된 헤더를 제거하여 상위 계층인 네트워크 계층으로 전달합니다.
- 사용하는 대표적인 장비로는 LAN 관련 장비, 프로토콜에는 Ehternet(이더넷), Token Ring, PPP 등이 있습니다.

OSI/ TCP 차이

OSI 7 Layer에서는 Presentation 계층에서 캡슐화를 하지 않고 Compression을 한다. 이것이 OSI와 TCP/IP의 차이점이다.

# 계층을 통과하는 데이터 송신

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d7f0972d-e04e-4f33-bbdf-296fe5714496/Untitled.png)

각 계층을 지나면서 해야할 일을 헤더에 붙이는 작업을 데이터 **캡슐화(Encapsulation)**

데이터를 보낼 때는 데이터 앞부분에 전송에 필요한 정보를 붙여서 다음 계층으로 전달한다. 이때 정보를 **헤더**
라고 하며, 헤더에는 데이터를 전달받는 상대에 대한 정보도 포함되어 있다.

이처럼 헤더를 데이터에 붙이는 것을 **캡슐화**
라고 한다. 반대로 데이터를 수신하는 측에서는 헤더를 하나씩 제거해야하며 이를 **역캡슐화**
라고 한다.

예) 로그인 ⇒ 사용자 아이디 + 비밀번호 = 데이터

application ⇒ 데이터

transport ⇒ 데이터 + 통신 정보

network ⇒ 데이터 + 통신 정보 + 네트워크 정보

Data Link ⇒ 데이터 + 통신 정보 + 네트워크 정보 + 트레일러 + 패킷

첫 번째, 먼저 응용 계층에서 요청 데이터(사용자가 필요한 정보)가 만들어집니다.

두 번째, 전송 계층에서 신뢰할 수 있는 통신을 구현하기 위해 header를 위에서 받은 데이터에 붙입니다.

header가 붙은 데이터를 세그먼트라고 하는 것이죠.

세 번째, 네트워크 계층에서는 다른 네트워크와 통신할 수 하는 header를 위에서 받은 세그먼트에 붙입니다. 이렇게 만들어진 데이터를 패킷이라고 하죠.

네 번째, 데이터 링크와 물리계층 즉, TCP/IP 계층에서의 네트워크 액세스 계층에서는 물리적인 통신 채널을 열기 위해서 위에서 받은 패킷에 헤더와 와 트레일러를 붙입니다. 트레일러는 데이터를 전달할 때 데이터 끝 부분에 붙이는 정보로, 에러 검출에 사용되죠. 이렇게 만들어진 데이터를 프레임이라고 합니다.

마지막, 이렇게 만들어진 프레임을 물리계층에서 비트로 구성된 전기 신호로 변환해서 데이터를 수신하는 컴퓨터에 전송하게 되는 것이죠.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7420753e-6f95-411b-88d3-987145adad9e/Untitled.png)

- 데이터 송신 측 컴퓨터에서 웹 사이트에 접속하려면 접속을 위한 요청 데이터가 만들어진다.
- 이 데이터는 전송 계층에 전달되며, 신뢰할 수 있는 통신이 이루어지도록 데이터에 헤더를 붙인다.
- 이 데이터 및 헤더는 네트워크 계층에 전달되며, 다른 네터워크와 통신하기 위한 헤더를 붙인다.
- 이 데이터 및 헤더는 데이터 링크 계층에 전달되며, 물리적 통신 채널을 연결하기 위한 헤더와 트레일러를 붙인다. 트레일러란 데이터를 전달할 때 마지막에 추가하는 정보를 말한다.
- 이 데이터 및 헤더는 최종적으로 물리 계층에서 전기 신호로 변환되어 수신 측에 전송한다.
- 수신 측은 데이터 링크 계층에서 응용 계층 순서로 데이터를 전달하며 각 계층에서 헤더를 제거한다. 응용 계층은 최종적으로 모든 헤더가 제거된 데이터를 받는다.
