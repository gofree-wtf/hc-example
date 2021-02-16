hc-example
==========

Apple HomeKit 악세사리를 만들 수 있는 [brutella/hc](https://github.com/brutella/hc) 라이브러리를 테스트해봅니다.

## Notes

> HomeKit에 대한 정확한 설명은 애플 개발자 [문서](https://developer.apple.com/homekit) 를 참고하세요.
> 아래는 단순히 에제 코드를 돌려본 결과에 대한 추측입니다.

- 예제 코드를 실행하면, 같은 네트워크 내에 있는 홈 허브에서 바로 인식한다.
  1. 홈 허브가  `POST /pair-setup`를 요청
  2. 홈 허브에서 PIN 코드를 입력
  3. 홈 허브가 `POST /pair-setup`을 요청
  4. 페어링 완료
- 예제 코드와 홈허브 간에 쌍방향 통신이 이루어진다.
  - 홈허브에서 아이콘 등을 탭하면 --> 예제 코드로 `PUT /characteristics`과 같은 이벤트가 온다.
  - 예제 코드에서 상태 등을 변경하면 --> 홈허브에 `EVENT/1.0 200 OK`과 같은 이벤트를 보낸다.
- 여러개의 악세서리를 추가할 수 있다.
  - 악세서리 별로 홈허브와 이벤트를 주고받을 수 있다.
  - 악세서리 타입은 정해져있는 것 같다.
    - https://github.com/brutella/hc/blob/master/accessory/constant.go
    - 악세서리 타입에 맞춰 홈허브에 아이콘이 표시된다.
  - 악세사리 타입 별로 이벤트가 정해져있는 것 같다.
    - 스위치의 경우: On/Off 제어만 가능
    - TV의 경우: https://github.com/brutella/hc/blob/master/_example/tv/main.go#L67-L134
