# 프론트엔드 면접 준비

## 면접 중요도 (하)

### graphQL 이란?

#### graphQL이란?

Graph QL(이하 gql)은 Structed Query Language(이하 sql)와 마찬가지로 쿼리 언어입니다.  
`sql`이란 데이터베이스에서 데이터를 효과적으로 가져오는것이 목적이고, `gql`은 은 웹 클라이언트가 데이터를 서버로 부터 효율적으로 가져오는 것이 목적이다.

#### REST API와의 차이점?

REST API는 URL, METHOD등을 조합하기 때문에 다양한 Endpoint가 존재 합니다. 반면, gql은 단 하나의 Endpoint가 존재 합니다. 또한, gql API에서는 불러오는 데이터의 종류를 쿼리 조합을 통해서 결정 합니다. 예를 들면, REST API에서는 각 Endpoint마다 데이터베이스 SQL 쿼리가 달라지는 반면, gql API는 gql 스키마의 타입마다 데이터베이스 SQL 쿼리가 달라집니다.

[출처: GraphQL 개념잡기](https://tech.kakao.com/2019/08/01/graphql-basic/)
