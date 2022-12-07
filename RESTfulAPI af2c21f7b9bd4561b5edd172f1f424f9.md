# RESTfulAPI

- RESTfulAPI
    - 프론트엔드와 백엔드가 소통하는 엔드포인트
    - 앱이나 웹 상에서 작동하는 어플리케이션 개발시 HTTP나 HTTPS 프로토콜을 사용하여 API를 만든다.
    - API 정의가 얼마나 직관적이고 명확한지에 따라 프로젝트의 복잡도가 크게 낮아지며 시스템 설계에 있어서 중요한 자리를 차지한다.
    - 일종의 약속을 통해 API를 정의한다.
        - HTTP 메소드와 URI(Uniform Resource Identifiers)이다.
        - 사용자가 표현을 읽고 API에게 기대하는 동작과 서버로 수행하는 동작을 일치시켜야 한다.
- REST가 의미하는 것은 무엇인가?
    - **RE**presentational **S**tate **T**ransfer
    - 대표적인 상태 ⇒ 표현된 상태로 해석할 수 있다.
        - 리소스의 상태를 얘기한다.
    - 통신을 통해 자원의 표현된 상태를 주고받는 것에 대한 아키텍처 가이드라인.
- 통신을 주고 받는 것은 리소스가 아니다.
    
    ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled.png)
    
    - 클라이언트가 서버에게 특정 유저의 정보를 받아오는 API 엔드포인트를 통해 요청
    
    ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%201.png)
    
    - 편의상 우리는 이 상황을 **`/api/users/2`**
    라는 엔드포인트를 통해서 2번 유저 데이터 리소스를 받아왔다고 표현하지만, 유저의 리소스가 아니다.
    - 서버가 보내준 JSON은 단지 데이터베이스에 저장되어 있는 원본 데이터 리소스의 현재 상태를 표현.

![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%202.png)

- URI
    - API가 어떤 리소스에 대한 API인지를 나타내는 요소
    - RESTful API는 이러한 리소스 간의 계층 구조를 **`/`**
    를 사용하여 표현할 것을 권장
    
    ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%203.png)
    
    ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%204.png)
    
    - 상위 계층 리소스를 정할 때 어떤 게 더 명확하냐에 따라 URI를 설계를 할 수 있다.
    - RESTful API는 URI를 사용하여 행위를 표현하지 않을 것을 권고
    - 올바르게 작성된 엔드포인트는 삭제를 의미하는 HTTP 메소드인 **`DELETE`**를 사용한 요런 엔드포인트가 될 것이다.
    
    ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%205.png)
    
    - API를 사용하여 하게되는 행위는 대부분 **`CRUD(Create, Read, Update, Delete)`** 이기 때문에, 몇 가지 특수한 경우를 제외하면 단 5가지의 HTTP 메소드만으로도 대부분의 API를 정의할 수 있다.
    
    ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%206.png)
    
    - **PUT과 PATCH의 차이**
        - **`PUT`**
         메소드를 사용하여 이 리소스를 수정한다면 우리는 반드시 요청 바디에 유저 리소스 전체를 표현하여 보내야한다.
        
        ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%207.png)
        
        - PUT 메소드는 리소스를 수정하는 것이 아니라 대체하는 것이다
        - **`PATCH`**
         PATCH 메소드는 리소스의 일부분을 수정하는 것이다
        
        ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%208.png)
        
        - **`PUT`** 메소드와 다르게 **`PATCH`**메소드는 진짜로 현재 저장되어 있는 리소스에 수정을 가하는 행위를 의미하기 때문에 굳이 수정하지 않은 사항을 요청 바디에 담아줄 필요도 없다.
        - 그러나 **`PUT`** 메소드와 **`PATCH`** 메소드의 진짜 중요한 차이점은
            
            이런 행위의 의미가 아니라, **`PUT`**메소드는 반드시 멱등성을 보장하지만 **`PATCH`** 메소드는 멱등성을 보장하지 않을 수도 있다는 것이다.
            
            - **`멱등성`**이란, 수학이나 전산학에서 어떤 대상에 같은 연산을 여러 번 적용해도 결과가 달라지지 않는 성질
            - 대표적으로 멱등성이 보장되는 연산은 바로 어떠한 수에 1을 곱하는 연산
            - **`x => x * 1`**
            과 같은 함수는 어떠한 값에 1번을 적용하든, 10,000번을 적용하든 항상 **`x`**를 반환한다.
        - HTTP 메소드 또한 결국 어떠한 자원을 읽고 쓰고 수정하고 지우는 CRUD에 대한 의미를 가지기 때문에, 우리는 어떤 행위가 멱등성을 보장하고 어떤 행위가 멱등성을 보장하는지 알고 있어야 어플리케이션이 예상하지 못한 방향으로 동작하는 것을 방지
        
        ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%209.png)
        
        - **`POST`**
         메소드의 경우 리소스를 새롭게 생성하는 행위를 의미하기 때문에 여러 번 수행하게 되면 매번 새로운 리소스가 생성
        - **`GET`**을 여러 번 수행했을 때 발생하는 에러와 **`POST`**를 여러 번 수행했을 때 발생하는 에러는 전혀 다른 컨텍스트를 가지고 있을 수 있다는 것
        - **`PATCH` 를 이런식으로 사용하면 멱등성이 보장 x**
        
        ![Untitled](RESTfulAPI%20af2c21f7b9bd4561b5edd172f1f424f9/Untitled%2010.png)
        
        출처:[https://evan-moon.github.io/2020/04/07/about-restful-api/](https://evan-moon.github.io/2020/04/07/about-restful-api/)