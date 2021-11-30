## Base 64 encoding
- Binary Data를 Text로 변경하는 Encoding

- 사용법
 1. 기존 문자열을 아스키 Binary Data로 바꾼 후 6bit씩 나눈다
 2. 6비트마다 Base 64 encoding을 실시한다.
 3. 문자열이 항상 3개씩 남김없이 끊어진다는 보장이 없기 때문에 남은 부분은 padding으로 =가 빈자리만큼 들어가게 된다.

- 사용 이유
  - Base 64 encoding을 하게 되면 전송해야 될 데이터양도 약 33% 정도 늘어난다.(6bit당 2bit의 overhead가 발생하기 때문)
  - 그럼에도 불구하고 아스키로만 encoding 후 데이터를 전송하면 여러 문제점이 있어 안전하지가 않기 때문에 base 64 encoding을 사용한다
    - 아스키는 7 bits encoding인데 나머지 1 bit를 처리하는 방식이 시스템 별로 상이
    - 일부 제어문자는 시스템 별로 다른 코드값 보유


- 정리
 Base64는 HTML 또는 Email과 같이 문자를 위한 Media에 Binary Data를 포함해야 될 필요가 있을 때, 포함된 Binary Data가 시스템 독립적으로 동일하게 전송 또는 저장되는걸 보장하기 위해 사용한다