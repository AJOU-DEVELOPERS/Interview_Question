## **컴파일러**

## AST ( 추상 구문 트리 )

- AST란?
    - 컴파일러에 사용되는 자료 구조로 일반적으로 컴파일러의 구문 분석 단계의 결과물.
    - 프로그래밍 언어에서 구문 분석의 모호함을 피하게 해준다.
- tokenizer 역할
    - 들어온 input 데이터를 알맞은 토큰 단위로 나뉘어주는 역할
- lexer 역할
    - 위에서 나눠진 토큰들을 분석하여 문맥적 의미를 부여( 숫자, 기호 등)
- parser 역할
    - 문맥적 의미가 부여된 토큰들을  문법적으로 검사하고 parse tree를 만들어준다.
    - 이 때, parse tree는 input 데이터 전체를 구체적으로 표현(공백, 괄호까지)
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cf18598d-8d8c-4a7d-ac5b-f6b11a54fd5f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cf18598d-8d8c-4a7d-ac5b-f6b11a54fd5f/Untitled.png)
    
- AST
    - 위의 pare tree에서 필수적인 정보만 담은 트리를 AST라고 한다.
    - AST는 input을 축항햐여 표현하였기 때문에 parse tree와 다르게 부모가 없고 괄호, 공백이 들어가지 않는다.
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b7c8154-7783-444b-824d-a052960c57e5/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b7c8154-7783-444b-824d-a052960c57e5/Untitled.png)