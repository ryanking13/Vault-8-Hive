원문 : https://wikileaks.org/vault8/#Hive

---

## Hive

_Hive_ 는 CIA 멀웨어 공격자들의 중요한 문제를 해결하기 위해 만들어졌다.

아무리 멀웨어를 정교하게 만들어 타겟의 컴퓨터에 심더라도, 공격자와 은밀하고 안전하게 통신할 수 있는 방법이 없다면 아무 소용이 없다. _Hive_ 를 사용하면, 만약 타겟이 자신의 컴퓨터에 심어진 멀웨어를 발견하고, 그것이 외부 서버와 통신한다는 것을 발견하더라도, CIA와의 연관성을 찾기 어렵게 만든다. _Hive_ 는, CIA의 멀웨어가 정보를 빼내어 CIA의 서버로 전송하도록 하고, 새로운 오퍼레이션(operation)을 받을 수 있도록하는 은밀한 통신 플랫폼이다.

_Hive_ 는 타켓 컴퓨터에 심어진 여러 멀웨어를 통해 여러 오퍼레이션을 수행할 수 있다. 각각의 오퍼레이션은 하나 이상의 커버 도메인(cover domain, e.g. "perfectly-boring-lookin-domain.com")과 통신한다. 각 도메인 웹사이트 서버는 상용 호스팅 업체로부터 구매한 VPS(virtual private server)를 사용한다. 이 서버들은 릴레이(relay) 역할을 하며, '숨겨진' CIA 서버(_Blot_)와 VPN 연결을 통해 데이터를 전송한다.

![Hive Structure](https://wikileaks.org/hive.png)

<br>

각 커버 도메인들은 일반 사용자가 우연히 접근하는 것을 대비하여 무해한(innocent) 정보를 제공함으로써, 일반적인 웹사이트처럼 가장한다. 이 사이트의 유일한 특색은, 일반 유저(non-technical users)는 모르는 HTTPS _Optional Client Authentication_ 옵션을 사용한다는 것이다. _Optional Client Authentication_ 은 일반적으로는 잘 사용되지 않는 옵션인데, _Hive_ 는 이를 이용한다. 이 옵션은 _Optional_ 하므로 일반 유저들은 인증(authenticate)을 요구받지 않지만, 멀웨어들은 자기자신을 인증함으로써 _Blot_  서버에 인지된다. 멀웨어가 보내는 트래픽(traffic)은 _Honeycomb_ 이라고하는 게이트웨이로 보내지며, 다른 트래픽은 무해한 데이터를 유저에게 제공하는 커버 서버(cover server)로 전송된다.

인증을 위한 인증서(Digital certificates)는 실제로 존재하는 인증서를 위조한 가짜 인증서를 생성하여 사용한다. 공개한 소스 코드에는 카스퍼스키 랩(Kasperskey Laboratory, Moskow)가 Thawte Premium Server CA, Cape Town으로 부터 인증받은 가짜 인증서를 생성하는 코드가 포함되어 있다. 이러한 방식을 통해, 만약 타겟이 네트워크 트래픽을 살펴보더라도, CIA의 관련성에 대해 알기 어렵게 만든다.
