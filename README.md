# shopping-app
# Getting Started

### Reference Documentation
For further reference, please consider the following sections:

* [Official Gradle documentation](https://docs.gradle.org)
* [Spring Boot Gradle Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/2.7.3/gradle-plugin/reference/html/)
* [Create an OCI image](https://docs.spring.io/spring-boot/docs/2.7.3/gradle-plugin/reference/html/#build-image)
* [Spring Web](https://docs.spring.io/spring-boot/docs/2.7.3/reference/htmlsingle/#web)
* [Spring Boot DevTools](https://docs.spring.io/spring-boot/docs/2.7.3/reference/htmlsingle/#using.devtools)
* [Spring Data JPA](https://docs.spring.io/spring-boot/docs/2.7.3/reference/htmlsingle/#data.sql.jpa-and-spring-data)

### Guides
The following guides illustrate how to use some features concretely:

* [Building a RESTful Web Service](https://spring.io/guides/gs/rest-service/)
* [Serving Web Content with Spring MVC](https://spring.io/guides/gs/serving-web-content/)
* [Building REST services with Spring](https://spring.io/guides/tutorials/rest/)
* [Accessing Data with JPA](https://spring.io/guides/gs/accessing-data-jpa/)

### Additional Links
These additional references should also help you:

* [Gradle Build Scans – insights for your project's build](https://scans.gradle.com#gradle)

# Requirements

## 선택1- 포인트 시스템 만들기 by Ethereum

- Spring boot or Node  + Web3 + 이더리움(Solidity) (DApp이라 지칭)

****포인트 시스템을 만들기 위한 시나리오는 간단하다. DB or Ethereum에는 제휴사(상품), 고객, 주문 스키마가 있고,  고객은 돈이나 포인트를 지불하여 제휴사의 상품을 구매할 수 있다.****

![image.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/41e52114-290b-4110-9b24-53c88cc20f43/image.png)

고객은 자신의 이름, 보유 자산, 보유 포인트를 저장하고 있다.

![image (1).png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/59a82eba-4e6a-42d7-9a5c-852f7ca783a6/image_(1).png)

상품은 상품 ID, 상품명, 개당 가격, 보유 개수, 포인트 비율, 소유자의 이름을 저장한다. 고객은 돈이나 포인트를 지불하여 상품을 구매할 수 있으며, 돈을 지불 하였을 경우에는 포인트를 적립 받는다. 포인트로 구매 하였을 경우에는 추가 포인트를 적립 받지 못하고 상품만 구매할 수 있다.

![image (2).png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/52879ece-2a2d-4d82-b75a-f21c6e9fd6aa/image_(2).png)

- 사용자와 상품에 대한 쿼리 기능도 추가합니다.
- 주요 테이블 구성 요소로는 사용자/상품/주문 정보가 있습니다.
- 주문에는 여러개의 상품이 들어 있을 수 있습니다.
- 주문취소는 안만들어도 됩니다.

위 시나리오를 갖는 DApp을 개발한다. (Rest API로 노출하며, 프론트엔드는 생략)

### 

## 선택2- 포인트 시스템 만들기 by JPA,H2 or MySQL

- 스프링부트 + JPA + RDB (App이라고 지칭)

선택1의 비지니스 로직에 추가적으로  장바구니 기능을 추가 합니다.
장바구니는 아래와 같은 기본 기능을 갖고 있습니다.

1. 장바구니와 고객은 1대1 단방향 매핑됩니다.

2. 상품을 장바구니에 추가/제거 합니다.  (상품과 장바구니는 중간엔터티를 두어 1대다, 다대1로 분리하여 처리합니다.)
3. 장바구니에 있는 것을 한번에 모두 주문 가능 하게 합니다.

# DB schema
User
- id
- email
- password
- name
- cash
- point
- created_at
- is_admin
- 

Product
- id
- name
- price
- quantity
- rate
- owner
- created_at

Order
- id
- user_id
- total_price
- purchase_type > point or cash
- accumulation
- created_at


Cart
- id
- user_id
- product_id
- quantity
- created_at

user 1:1 cart 1:N cart_product N:1 product

order cart 1:1
user 1:N order 1:N order_product N:1 product


Spring boot mysql jpa lombok

## API

get users
create user
update{id} user
delete{id} user
get{id} user

get products
get{id} product
update product
- price
- quantity
- 
