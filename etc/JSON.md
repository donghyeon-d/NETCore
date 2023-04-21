# JSON(JavaScript Object Notation)

## 의미
*  이름에서 알 수 있듯, JavaScript에서 객체를 만들 때 사용하는 문법을 기반으로 만들어짐 
* 하나의 문자열로 취급할 수 있고 양식과 구조가 정해져 있어서  경량의 데이터 교환 형식으로 사용됨
* 객체와 배열 등의 데이터를 표현할 수도 있고, key-value pair 방식을 사용하여 데이터를 표현함
* 가독성이 높고 파싱하기 쉬우며 전송 속도가 빠름
* 규칙을 갖는 단순한 텍스트 포맷으로 취급할 수 있기에 다양한 언어에서 이 포맷을 사용할 수 있음

## 문법
* 텍스트 기반으로 구조화된 데이터를 표현함
### 1. 데이터 타입
* 문자열(string), 숫자(number), 객체(object), 배열(array), 불리언(bool - true,false), null을 사용함
* 모든 key와 value는 각각 쌍따옴표 ""로 둘러싸여 있음
### 2. 객체(object)
* 중괄호 {} 로 둘러싸인 key-value 쌍의 집합
* 각 key와 value은 콜론 ':' 으로 구분되고, 콜론 뒤에 공백을 넣음
* key는 반드시 string 타입이어야 하고, value는 1에서 기술한 모든 데이터 타입을 가질 수 있음
* 여러개의 key-value 쌍이 있으면, 콤마 ','로 구분함
``` JSON
객체 (object)
{
    "name": "John",
    "age": 30,
    "address": {
        "city": "New York",
        "state": "NY"
    },
    "hobbies": ["reading", "music", "traveling"]
}
```
### 3. 배열(array)
* 대괄호 []로 둘러싸인 값들의 집합
* 1에서 기술한 모든 데이터 타입 중 한가지로 배열을 표현할 수 있음
* 값들은 콤마 ','로 구분함
* 2번 객체의 코드에서 `"hobbies"` 는 배열임(문자열의 배열)
``` JSON
객체의 배열
[
    {
        "name": "John",
        "age": 30
    },
    {
        "name": "Jane",
        "age": 25
    },
    {
        "name": "Mark",
        "age": 35
    }
]
```
### 4. 주석(comment)
* JSON에서는 주석을 사용할 수 없음 (# // 등 )
* 주석 대신에 "comment"라는 key에 "원하는 내용"을 value로 넣기도 함
``` JSON
주석 comment
{
    "name": "John",
    "age": 30,
    "comment": "This is a comment."
}
```

## 참고문헌
* [oracle](https://www.oracle.com/kr/database/what-is-json/)
* [json.org](https://www.json.org/json-ko.html)
* [itworld](https://www.itworld.co.kr/news/252478)