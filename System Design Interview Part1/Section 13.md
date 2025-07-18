# 검색어 자동완성 시스템
## 1단계 - 문제 이 및 설계 범위 확정
#### **요구사항**
* 빠른 응답속도 : 사용자가 검색어를 입력함에 따라 자동완성 검색어도 빠르게 표시되어야 한다.
* 연관성 : 자동완성되어 출력되는 검색어는 사용자가 입력한 단어와 연관된 것이어야 한다.
* 정렬 : 시스템의 계산 결과는 인기도 등의 순위 모델에 의해 정렬되어 있어야 한다.
* 규모 확장성 : 시스템은 많은 트래픽을 감당할 수 있도록 확장 가능해야 한다.
* 고가용성 : 시스템의 일부에 장애가 발생하거나 느려지거나, 예상치 못한 네트워크 문제가 생겨도 시스템은 계속 사용 가능해야 한다.

#### **개략적 규모추정**
* 일간 능동 사용자(DAU)는 천만 명으로 가정한다.
* 평균적으로 한 사용자는 매일 10건의 검색을 수행한다고 가정한다.
* 질의할 때마다 평균적으로 20바이트의 데이터를 입력한다고 가정한다.
    * 문자 인코딩 방법으로는 ASCII를 사용한다고 가정할 것이므로, 1문자 = 1바이트이다.
    * 질의문은 평균적으로 4개 단어로 이루어진다고 가정하고, 각 단어는 평균적으로 다섯 글자로 구성된다고 가정할 것이다.
    * 따라서 질의당 평균 4 X 5 = 20바이트이다.
* 검색창에 글자를 입력할 때마다 클라이언트는 검색어 자동완성 백엔드에 요청을 보낸다. 따라서 평균적으로 1회 검색당 20건의 요청이 백엔드로 전달된다.
* 대략 초당 24,000건의 질의(QPS)가 발생할 것이다.
* 최대 QPS=QPS x 2=대략 48,000
* 질의 가운데 20% 정도는 신규 검색어라고 가정할 것이다. 따라서 대략 0.4GB정도로, 매일 0.4GB의 신규 데이터가 시스템에 추가된다는 뜻이다.

## 2단계 - 개략적 설계안 제시 및 동의 구하기
