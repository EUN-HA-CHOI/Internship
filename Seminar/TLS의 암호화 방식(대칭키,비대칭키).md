## TLS의 암호화 방식(대칭키,비대칭키).   

SSL 은 웹사이트와 브라우저 사이에 전송된 데이터를 암호화하여 인터넷 연결 보안을 유지하는 표준 기술이다. 이는 해커가 개인 정보 및
금융 정보를 포함한 전송되는 모든 정보를 열람하거나 훔치는 것을 방지한다.

쉽게 말해, 네트워크 통신을 할 때 보안을 제공하기 위해 설계된 암호 규약이다. TCP/IP 네트워크를 사용하는 통신에 적용 된다.
TLS 는 SSL 과 같다. 처음에 네스케이프 사에 의해 발명된 SSL이 표준화가 되며 바뀐 이름이 TLS이다. TLS 라는 이름은 생소하여 SSL이
더 널리 쓰이긴 한다.

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/e703d175-d9aa-4cc3-831e-eb5d2bc91d5e)
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/8e83b415-b15c-4d65-903a-f1a97c5dd8d4)


HTTP 와 HTTPS 의 차이점에 대하여 알아보자. 먼저, HTTP 는 암호화 되지 않은 평문으로 데이터를 전송함. 따라서 누군가 패킷을 훔쳐
보는 스니핑 공격에 취약함. HTTP 통신에선 Wire Shark 를 통해 패킷을 확인하면 내 주민번호가 그대로 서버로 전송되는 것을 볼 수 있다.
누가 패킷을 훔펴보면 내 주민번호가 그대로 털림.

때문에, 서버와 클라이언트 간 데이터를 보호하기 위해선 인증서를 통해 패킷을 암호화 한 뒤 전송해야 된다. 이때 사용하는 보안 인증(암
호화 + 서버인증 등)이 TLS 이다. 즉, HTTPS는 TLS 프로토콜 위에서 돌아가는 HTTP 프로토콜이다.

<hr>

- 암호화
TCP/IP/ 통신을 할 땐 데이터를 암호화 하는 보안이 필요하고, 그 보안 인증에 TLS가 있다는 것을 알았으니 TLS는 어떻게 데이터를 암호
화 할까? 먼저, TLS는 보안과 성능상 이슈로 두 가지의 암호화 방법을 혼용해서 사용한다. 대칭키,비대칭키 암호화이다.

암호화라는 것은 무엇인가 남들은 읽을 수 없게, 비밀이 유지되어야 할 때 사용하니까 암호화를 하기 위해선 일종의 키가 필요하다. 키는
문자나 숫자가 될 수도 있어 마음대로 정할 수 있다.

암호화는 그냥 하는 것이 아니라 이 키 + 데이터를 이용하여 암호화 된 데이터를 만들어 내는 것이다. 따라서 키가 단 한 글자라도 다르다
면 암호화의 내용도 전혀 달라진다.

복호화 또한 마찬가지로 암호화된 데이터 + 키를 이용하여 데이터를 얻는 것이다. 때문에 보호화에서도 키는 필요하다. 키를 모른다면 절
대 복호화를 할 수 없다.

이때 암호화 복호화에 사용하는 이 키는 서로 동일 할 수도, 다를 수도 있다.

<hr>

- 대칭키 암호화 
먼저 대칭키 암호화란, 암호화를 하는 키와 복호화를 하는 키가 동일한 방식이다. 이때 암호화와 복호화에 동시에 사용되는 이 키를 대칭
키 라고 한다. 
 ![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/bc6957cc-f098-4636-a11e-96a44d605074)
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/fa25b3a4-b612-489c-88d3-b346b9d79651)

- 대칭키 암호화 예시 
“2699” 이라는 키로 암호화 복호화를 동시에 하고 있다. 그렇다면 이 커플은 대칭키 “2699”을 이용힌 대칭키 암호화를 사용하고 있는 것
이다.
여기서 대칭키 암호화의 단점이 드러난다.

대칭키는 상대방도 나도 서로 공유를 해야하기 때문에, 대칭키를 전달하는 과정에서 누가 훔쳐볼 위험이 있다. 만약 대칭키가 해킹당한
다면 당연히 복호화가 가능하니, 데이터도 누출되게 된다.

이처럼 대칭키 암호화 방식에선, 대칭키를 상대에게 전달하는 방식에서 해킹당할 리스크가 있다. 이러한 대칭키 암호화의 근본적인 문제
를 해결하고자 나온것이 비대칭키 암호화 방식이다.

<hr>

- 비대칭키 암호화  
하나의 키를 갖는 대칭키 암호화 방식과 달리, 비대칭키 암호화 방식은 한 쌍의 키를 갖게 된다. 한 마디로 비대칭키 암호화 방식에선 키
가 2개이다. 이 두 개의 키로 각각 암호화, 복호화를 할 수 있다. 만일 A,B 라는 두 개의 키가 있다면 A키로 암호화한 데이터는 B키로만 복
호화를 할 수 있다. 또한 B키로 암호화한 데이터는 A키로만 복호화를 할 수 있다. A키로 암호화한 데이터를 A키로 복호화 할 순 없으며,
B키도 마찬가지이다.

통상적으로 비대칭키 방식에서 가지는 두 개의 키에서 하나는 공개키,하나는 개인키 라고 부른다. 이렇기 때문에 공개키는 암호화를, 개
인키는 복호화를 한다고 알려져 있는데 그렇지 않다.

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/4b12d51c-b4f8-43ed-bdfc-070f01d86b95)

- RSA 알고리즘
공개키로 암호화 하면 개인키로 복호화 할 수 있고, 개인키로 암호화 하면 공개키로 복호화 할 수 있다. 이렇듯 한 쌍의 키로 암호화, 복호
화를 하는 방식을 RSA 알고리즘 이라고 한다. 그럼 이 알고리즘을 통해 어떻게 데이터를 암호화,복호화 하여 주고 받는지 알아보자

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/73b326f6-d3b9-49cd-9e38-67b4aa9f260d)

- RSA 알고리즘 예시
남자와 여자가 RSA 알고리즘을 통해 메세지를 주고 받는다. 그렇다면 남자는 공개키와 개인키를 가질 것이고, 여자 또한 공개키와 개인
키를 가질 것이다. 이제 여자는 남자에게 자신의 공개키를 알려주고, 남자도 여자에게 자신의 공개키를 알려준다. 이 과정에서 공개키가
해킹당한다 해도 개인키를 알지 못하면 복호화를 할 수 없어 안전하다. 그러면 남자의 공개키를 받은 여자는 전송하고자 하는 메시지를
남자의 공개키로 암호화 하여 전송한다. 그러면 남자는 받은 데이터를 자신의 개인키로 복호화 하여 볼 수 있다. 반대로 남자가 여자에게
데이터를 보낼 땐 여자의 공개키로 암호화를 해서 보내고, 여자는 받은 데이터를 자신의 개인키로 복호화 하여 보는 것이다.

왜 TLS 는 대칭키 방식과 비대칭키 방식을 같이 사용할까? 그 이유는 RSA 알고리즘을 이용한 암호화 방식은 복잡한 수학적 원리로 이루
어져 있어 CPU 리소스를 크게 소모한다는 단점이 있다. 이 때문에. RSA 비대칭키 방식으로만 통신을 하기에 성능상 어려움이 있다.

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/03493cbb-2549-4287-a74f-c9b712537e69)

<hr>

- TLS 암호화 방식
대칭키 방식과 비대칭키 방식의 원리를 알아보았다. 위에서 설명한 두 방식의 단점 때문에, TLS에서는 이 두 가지 방식을 보완하여 사용
한다.
대칭키 방식에서의 가장 큰 문제점은 대칭키를 전달할 때 해킹당할 리스크인데 이를 RSA 비대칭키 방식으로 보안한 것이다.
처음에 대칭키를 서로 공유하는 통신을 RSA 비대칭키 방식을 이용하고, 실제 통신을 할 때는 CPU 리소스 소모가 적은 대칭키 방식으로
데이터를 주고 받는다.

RSA 비대칭키 통신을 이용해 대칭키를 안전하게 전달할 수 있고, 이제부턴 대칭키를 해킹당할 일이 없으니 대칭키 방식을 이용해 통신을
하는 것이다.

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/72890487-1d66-4282-bb71-67c335f5980d)

- TLS 암호화 방식 예시
비대칭키 암호화 방식으로 대칭키 “1234”를 비밀스레 공유하고, 대칭키를 안전하게 공유 했으니 대칭키 암호화 하여 메세지를 주고 받는
내용이다.
인증서와 공개키가 조작 없이 무결한지 검증을 해야 된다. 

<hr>

- TLS 가 제공하는 이점들
1. 기밀성(암호화) 서버와 주고 받는 데이터가 스니핑 되는 것을 방지한다. 패킷이 오가는 것을 훔쳐 볼 순 있어도 안전하게 암호화 된 패
킷이라 복호화 할 수 업기 때문에 데이터는 훔쳐 볼 수 없다.

2. 데이터 무결성 - 통신 도중 데이터가 제 3자에 의해 악의로 변경될 일이 없다. 기밀성과 같은 선상에서 보면 된다. 서로의 대칭키를
RSA 알고리즘을 통해 안전하게 공유한 후에 암호화하여 통신하기 때문에 제 3자가 대칭키를 알아내지 않는 한 중간에서 암호화된 데
이터를 임의로 수정하지 못한다.

3. 서버인증 - 만약 암호화 방식으로만 서버와 클라이언트가 통신을 한다고 가정 하면 서버와 나는 암호화를 통해 통신하기 때문에 아무
도 데이터를 훔쳐볼 수도 건들 수도 없다. 근데 만약 서버가 신회할 수 없는 서버라면? 이처럼 서버와 클라이언트 간 통신을 할 때는
서버가 신뢰할 수 있는 서버라는 것을 확인하는 작업이 필요하다. 이럴 때 사용하는 것이 바로 '인증서'이다. 

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/43910fa8-885b-4ce0-a2aa-1077af12ba26)


- 인증서.   
서버가 신뢰할 수 있는 진짜 서버 임을 확인 하기 위해 필요한 것이 바로 인증서이다. 인증서에는 다음과 같은 정보들을 포함하고 있다. 

1.서비스 정보(인증서를 발급한 CA, 서비스의 도메인등) 
2. 서버 측 공개키(공개키, 공개키 암호화 방법)
3.  3. 지문, 디지털 서명 등 


