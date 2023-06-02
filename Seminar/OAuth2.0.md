## OAuth2.0.  

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/cfd4652f-f0b9-429d-8077-60a38a01384a)

웹 서핑을 하다 보면 구글과 페이스북 등의 외부 소셜 계정을 기반으로 간편히 회원가입 및 로그인 할 수 있는 웹 어플리케이션을 쉽게 찾
아볼 수 있다.

클릭 한 번으로 간편하게 로그인할 수 있을 뿐만 아니라, 연동되는 외부 웹 어플리케이션에서페이스북 및 트위터 등이 제공하는 기능을
간편하게 사용할 수 있다는 장점이 있다.

예를 들어, 구글로 로그인하면 API를 통해 연동된 계정의 구글 캘린더의 정보를 가져와 사용자에게 보여줄 수 있다. 이 때 사용되는 프로
토콜이 바로 OAuth 이다.

인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 어플리케이션의 접근 권한을 부여
할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 개방형 표준

예를 들어, 구글에 저장되어 있는 사용자의 연락처와 연동이 되는 어플리케이션을 만든다고 가정을 해 보자.어플리케이션 개발자로서 구
글에 저장되어 있는 사용자의 연락처 데이터를 어떻게 읽어올 수 있을까?

원시적인 방법은 사용자에게 직접 구글에 들어가서 자신의 연락처를 내려 받아 우리 어플리케이션에 올리라고 하는 것이다. 하지만 이런
방식으로는 여러 장치를 통해 시시각각 바뀌는 사용자의 연락처 정보를 실시간으로 업데이트를 받을 수가 없다. 또한 많은 사용자들은
직접 연락처를 업로드 하기가 너무 불편해서 애초에 이 어플리케이션을 쓰려고 하지도 않을 것이다.

두 번째 방법은 사용자에게 구글 계정의 이메일과 암호를 알려달라고 해서 사용자 대신 구글에 로그인 해서 사용자의 연락처를 읽어오는
것이다. 하지만 이럴 경우 기술적으로 사용자의 연락처 뿐만 아니라 지메일이나 구글 드라이브에 저장된 민감한 개인정보까지도 모두 접
근할 수 있게 되기 때문에 이는 보안적으로 위험한 발상이다. 또한 개인정보를 넘겨준다 해도 개발자 입장에서 이것을 안전하게 관리할
수 있을지 고민이 많아지게 됨.

이렇게 타 서비스에 저장된 사용자 데이터를 우리가 개발하는 어플리케이션으로 끌고 오는 것은 생각보다 쉽지 않습니다. 이러한 문제를
해결해주는 오어스2.0 을 사용하면 어플리케이션은 타 서비스에 저장된 사용자 데이터를 접근해도 되는지 사용자에게 명시적으로 허락
받을 수 있다. 사용자 입장에서도 자신의 모든 데이터가 아닌 특정 데이터의 특정 작업에 대해서만 접근을 허용할 수 있기에 안심하고 오
어스 2.0을 사용할 수 있다.


### OAuth 2.0 구성 요소  

- Resource Owner  
 서비스 제공자의 서비스(깃허브,페이스북,구글 등)에 가입되어 있어서 개인정보를 소유 중인 사용자, 내가 만든 앱을 사용할 사용자.
‘Resource’는 개인정보라고 생각하면 된다. 

- Client. 
  서비스 제공자에게 서비스를 제공받은 서버 또는 서비스를 말한다. 내가 만든 앱이라고 생각.
클라이언트 라는 이름은 Client 가 Resource Owner에게 필요한 자원을 요청하고 응답하는 관계여서 그렇다.

- Authorization Server 
  OAuth2.0 액세스 토큰을 발급 받기 위한 서비스 제공자의 인증 서버
  사용자는 이 서버로 ID, PW 를 넘겨 Authorization code 를 발급 받을 수 있다.
  Client 는 이 서버로 Authorization code 을 넘겨 token을 발급 받을 수 있다.
  
- Access Token 
  자원에 대한 접근 권한을 resource owner 가 인가하였음을 나타내는 자격증명 
  
- Refresh Token
Client 는 Authorizotion server로부터 access token(비교적 짧은 만료기간을 가짐)과 refresh token(비교적 긴 만료기간을 가짐)을 함께 부여 받는다.
Access token 은 보안상 만료기간이 짧기 때문에 얼마 지나지 않아 만료되면 사용자는 로그인을 다시 시도해야 한다.
그러나 refresh token 이 있다면 access token 이 만료될 때 refresh token을 통해 access token 을 재발급 받아 재 로그인 할 필요없게끔 한다.

<hr>

### OAuth 서비스 등록 해 보기 (NAVER 로그인). 
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/59936fae-03f1-4f5f-a2db-45445341455a)
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/61975e6f-ca47-418e-a87c-4b439ca44ffa)


### Resource owner 승인 과정 
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/1a54ac9c-a638-4f96-b314-715cc126a1f9)

1. 사용자(resource owner)는 서비스(client)를 이용하기 위해 로그인 페이지에 접근한다.
2. 그럼 서비스(client)는 사용자(resource owner)에게 로그인 페이지를 제공하게 된다. 로그인 페이지에서 사용자는 “페이스북으로 시작”
버튼을 누른다.

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/642843fe-d9fc-4a0b-b304-5cf4a4f82806)

브라우저 응답(response)헤더를 확인하면 다음 url 내용을 확인 할 수 있다.  

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/200a7e32-e728-4b64-83f8-d10c57abfed7)

사용자가 직접 페이스북으로 이동해서 로그인을 입력해야 하는데, 저 링크가 대신 로그인으로 이동 하게끔 도와준다.
향후 redirect_uri 경로를 통해서 resource server 는 client 에게 임시 비밀번호인 authorization code를 제공한다.

### 로그인 페이지 제공
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/6c69fa8b-9ecf-4a27-875f-ec724167b316)

ID/PW 를 적어서 로그인을 하게 되면, client가 사용하려는 기능(scope)에 대해 Resource Owner의 동의(승인)을 요청한다.
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/e39d4b77-bdf1-42c0-abb1-2a5445ca184c)

 Resource Owner가 Allow(동의) 버튼을 누르면 Resource Owner가 권한을 위임 했다는 승인이 Resource Server에 전달된다.
 
이로써 Resource Server가 갖는 정보는 다음과 같다.
- Client Id : Resource Owner와 연결된 client가 누군지
- Client Secret: Resource Owner와 연결된 client의 비밀번호
- Redirect URL : (진짜)client와 통신할 통로
- user id : client와 연결된 Resource Owner의 id
- scope : client가 Resource Owner 대신에 사용할 기능들

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/a86104f8-d883-4179-b999-b2f8deac1ffe)

하지만, 이미 Owner가 Client에게 권한 승인을 했더라도 아직 Server가 허락하지 않았다. 따라서, Resource Server 도 Client에게 권한 승
인을 하기 위해 Authorization code를 Redirect URL을 통해 사용자에게 응답하고

다시 사용자는 그대로 Client에게 다시 보낸다.

이를 통해, client는 Resource Server가 보낸 Authorization code, "code=3"를 Resource Owner통해 받는다.

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/cb49c995-06b8-4a29-9fdd-684c961d5420)

이제 client 가 Resource Server에게 직접 url(client id, pw, 인증코드 등)을 보낸다.

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/ae7bb367-d567-46a6-bf9b-5871db46b03d)

그럼 Resource Server 는 client 가 전달한 정보들을비교해서 일치한다면, Access Token을 발급한다. 그리고
이제 필요 없어진 Authorization code는 지운다.

그렇게 토큰을 받은 client는 사용자에게 최종적으로 로그인이 완료되었다고 응답한다.

**OAuth 의 목적은 Access Token을 발급 하는 것**. 

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/30c6ee38-73e5-424f-a9c8-1bf8386744b6)

이제 client 는 Resource server 의 api 를 요청해 Resource Owner의 ID 혹은 프로필 정보를 사용할 수 있다.

### Refresh Token
Access Token 이 기간이 만료되어 401 에러가 나면, Refresh Token 을 통해 Access Token을 재발급 한다.
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/1ce3ec96-e652-410b-ac9a-429157e39f74)

#### Refresh Token
protected resource 를 요청할 때는 꼭 액세스 토큰을 제시해야 한다. 토큰을 client 에게 발행된 인증에 관한 내용을 담는 암호화된 문자열이
다. 인증 범위나 인증 기간 등의 정보를 포함하는데, resource owner 에 의해 grant(허가) 되어야 하는 부분이다.

리프레시 토큰은 엑세스 토큰과 비슷한 형태를 띄고 있는데, 보통 액세스 토큰 보다 만료 기간이 길다는 차이가 있다. 이는 보안상의 문제
로 인한 절충안인데, 만약 만료 기간이 긴 토큰이 갈취당했을 경우 생각해보면 공격자는 해당 토큰이 만료되기 전까지는 protected
resource 를 마음껏 요청해서 받아올 수 있다. 이런 위험성을 줄이고자 엑세스 토큰의 만료 기간을 상대적으로 짧게 하고, 리프레시 토큰을
길게 한다. 그래서 액세스 토큰이 만료 되었을 때, 리프레시 토큰을 이용하여 새로운 엑세스 토큰 발급을 요청하게 된다.

Refresh Token의 발급 여부와 방법 및 갱신 주기 등은 OAuth를 제공하는 Resource Server마다 상이하다.
Access Token은 만료 기간이 있으며, 만료된 Access Token으로 API를 요청하면 401 에러가 발생한다.
Access Token이 만료되어 재발급 받을 때마다 서비스 이용자가 재 로그인하는 것은 다소 번거로울 것이다.

보통 Resource Server는 Access Token을 발급할 때 Refresh Token을 함께 발급한다.
Client는 두 Token을 모두 저장해두고, Resource Server의 API를 호출할 때는 Access Token을 사용한다.
Access Token이 만료되어 401 에러가 발생하면, Client는 보관 중이던 Refresh Token을 보내 새로운
Access Token을 발급받게 되어 로그인 인증을 유지 할 수 있게 된다.
