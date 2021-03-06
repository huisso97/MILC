### Solidity

- 함수에 사용하는 view, pure

  - view : 변수값을 변화시키지않고 불러오기만 할 때 사용, 가스 최적화를 말할 때 가장 중요한 내용
  - pure : 함수가 앱에서 어떤 데이터도 접근하지 않는 것을 의미

- Keccak256

  이더리움은 SHA3의 한 버전인 Keccak256를 내장 해시 함수로 가지고 있다.

  해시 함수는 기본적으로 입력 스트링을 랜덤 256비트 16진수로 매핑한다.

  스트링간의 동일 여부를 판단하기 위해 이용한다

  이방법은 안전하지는 않다

- mapping

  구조화된 데이터를 저장하는 방법 중 하나

  키-값 저장소

  데이터를 저장하고 검색하는데 이용

  예시) mapping (키=> 값) 이름;

- msg.sender

  현재 함수를 호출한 사람(혹은 스마트 컨트랙트)의 주소를 가리킨다

  솔리디티에서 함수 실행은 항상 외부 호출자가 시작한다. 따라서 항상  msg.sender가 존재한다

  이더리움 블록체인의 보안성을 이용할 수 있게 된다. 즉 누군가 다른 사람의 데이터를 변경하려면 해당 이더리움 주소와 관련된 개인키를 훔치는 것 밖에는 다른 방법이 없다는 것 이다.

- require

  특정 조건이 참이 아닐 때 함수가 에러 메시지를 발생하고 실행을 멈춘다

- storage vs memory

  - storage

    블록체인상에 영구적으로저장되는 변수

    함수 외부에 선언된 변수는 초기 설정상 storage로 됨

  - memory

    임시적으로 저장되는 변수

    함수 내에 선언된 변수로 함수 호출이 종료되면 사라진다

- internal external

  - internal

    함수가 정의된 컨트랙트를 상속하는 컨트랙트에서도 접근이 가능하다

    위 내용만 제외한다면 private와 동일

  - external

    함수가 컨트랙트 바깥에서만 호출될 수 있고 컨트랙트 내의 다른 함수에 의해 호출될 수 없다

    위 내용만 제외한다면  public과 동일

- 인터페이스

  블록체인 상에 있으면서 우리가 소유하지 않은 컨트랙트와 우리 컨트랙트가 상호작용을 하려면 인터페이스를 정의해야 한다

  contract 키워드를 이용하여 새로운 컨트랙트를 생성하는 것과 같이 인터페이스를 정의한다

- 컨트랙트의 불변성

  이더리움에 컨트랙트를 배포하고 나면, 컨트랙트는 변하지않는다. 즉 수정을 할수 없다는 것

  배포한 최초의 코드는 항상 존재한다. 이것이 솔리디티에 있어서 보안이 굉장히 큰 이슈인 이유이다.

- ownable컨트랙트

  OpenZeppelin 솔리디티 라이브러리의 컨트랙트

  컨트랙트의 생성자가 owner가 된다

  특정한 함수들에 대해서 오직 owner만 접근할수 있도록 제한 가능하다

  새로운 소유자에게 컨트랙트의 소유권을 옮길 수 있다

  대부분의 DApp들은 이것을 사용하고 첫 컨트랙트에 상속해서 사용한다

- 함수 제어자

  modifier

  직접 호출 불가

  함수 정의부 끝에 제어자의 이름을붙여 사용

- 가스

  솔리디티에서는 사용자들이 내가 만든 DApp의 함수를 실행할 때마다 가스를 지불해야한다

  함수의 로직이 얼마나 복잡한지에 따라 필요한 가스의 양이 정해진다

  코드 최적화가 중요한 이유는 사용자들의 가스 비용을 줄이기위해.

  - 구조체 내에서의 가스

    - uint의 하위 타입을 쓴다고 해서 가스를 절약하는것이 아니다. 이유는 솔리디티가 uint의 크기와 상관없이 256비트의 저장공간을 미리 잡아두기 때문이다. 하지만 구조체 안에서는 예외이다. 가능한 더 작은 크기의 uint를 사용하므로써 더 적은 공간을 차지하도록 압축된다

    - 동일한 데이터 타입은 같이 붙여 두는게 저장공간을 최소화한다

      ex) 1. uint; uint32; uint32;   2. uint 32; uint; uint32;  => 1번이 가스를덜 소모한다

- 시간 단위

  시간 단위에 해당하는 길이 만큼의 초단위를 uint 숫자로 변환된다

  now는 기본적으로 uint256을 반환한다

  ex) 1 days는 86400

- storage는 비싸다

  대부분의 프로그래밍 언어에서는 큰 데이터 집합의 개별 데이터에 모두 접근하는 것은 비용이 비싸다

  하지만 솔리디티에서는 그 접근이 external view 함수라면 storage를 사용하는 것보다 더 저렴한 방법이다.

  그이유는 view는 가스를 소모하지 않기 때문이다

- payable

  컨트랙트에 이더를 보내는 방법

  이더를 받을수 있는 특별한 함수 유형

- transfer

  특정한 이더리움 주소에 돈을 보낼 수있다

- this.balance

  컨트랙트에 저장되어있는 전체 잔액을 반환

- ERC20, ERC721

  - ERC20

    화폐처럼 사용되는 토큰으로 적절하다

  - ERC721

    교체 불가 - 이유는 각각의 토큰이 유일하고 분할이 불가하기 때문

    전체 단위로만 거래할 수 있고, 각각의 토큰은 유일한 ID를 가지고 있다

    - ERC721 표준

      - balanceOf : address를 받아 해당 address가 토큰을 얼마나 가지고 있는지 반환

      - ownerOf : 토큰ID를 받아 이를 소유하고 있는 사람의 address를 반환

      - transfer : 전송상대 address와 전송하려는 토큰id로 함수 호출

        ​                  takeOwnership과 동일한 전송 로직을 가지고 있기 때문에 이 로직만의 private 함수를 만들어 추상화하는것이 좋다.

        ​				  두함수에서 모두 쓸 수 있도록.

      - approve : 소유자가 새로운 소유자의 address와 그에게 보내고 싶은 _tokenId를 사용하여 호출

      - takeOwnership : 새로운 소유자가 토큰 아이디를 사용하여 호출, 컨트랙트는 그가 승인된 자인지 확인하고 토큰을 전송

- SafeMath

  오버플로우,언더플로우를 막기 위해 safeMath를 사용

  ex) using SafeMath for uint256

  library키워드를 사용해 using 키워드를 사용할 수 있게 해준다

- assert, require

  require는 함수 실행이 실패하면 남은 가스를 사용자에게 돌려주지만 assert는 그렇지않다

  따라서 assert는 코드가 심각하게 잘못 실행될 때 사용한다

  