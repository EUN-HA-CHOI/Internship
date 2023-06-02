### NET::ERR_CERT_AUTHORITY_INVALID 오류란?(인증서가 도메인과 일치하지 않을 때 발생)
브라우저가 웹사이트 SSL 인증서의 유효성을 확인할 수 없을 때 나타난다. 인증서를 설정하지 않았거나 웹사이트에 HTTP 를 사용하는
경우(권장되지 않음) 이 오류가 발생하지 않아야 한다.

유효하지 않은 인증 기관 오류에는 세 가지 주요 원인이 있다.
1. 자체 서명된 SSL 인증서를 사용하고 있다.
2. 인증서가 만료되었습니다.
3. 인증서는 신뢰할 수 없는 소스에서 가져온다.

사용자가 SSL 인증서가 있는 웹사이트를 방문할 때마다 브라우저에 이를 확인하고 해독해야 한다는 점을 기억해야 한다. 해당 프로세스
중에 오류가 있으면 경고가 표시된다.
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/e9f7dca7-8760-40a7-b8c5-edfe8f607367)

npm start 를 하니 AxiosError 가 떴다  

### 해결 방법  
1. 크롬 베타 다운 해서 접속. (오류)
2. 확장 프로그램 비활성(오류)
3. 디버깅(import 타입 외에 문제없음)
4. ChromeSetup (2).exe 다운 (오류)
5. node_modules 설치
6. tsconfig.json => "allowSyntheticDefaultImports": true, 입력

이유는 모르겠으나 해결 완료  

### Failed to load resource: net::ERR_CERT_AUTHORITY_INVALID
잘 돌아가다가 또 이 오류가 발생했다. 이유는 모르겠음
구글링 해 보다가 안 되겠어서 컴퓨터 다시 시작 하고 파일 다시 열기 해서 해결 완료 



