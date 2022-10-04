# JSON 이해하기

JSON은 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷이다.

spring에서는 주로 JSON을 이용해 데이터 통신을 한다.

JSON은 key:value 형태를 사용한다.

    {
    "key" : "value",
    "key" : "value"
    }

JSON은 네이밍 컨벤션으로 snake-case를 주로 사용한다.

ex)

spring_JSON

phone_number

---

### JSON에 오브젝트 넣기
{ } 를 열고 넣는다

```
{
    "account" : {
            "email" : "asdf@gmail.com",
            "username" : "yuns"
        }
}
```

### JSON에 배열 넣기
[ ] 를 열고 넣는다

```
{
    "user_list" : [
        {
            "account" : "asdf",
            "password" : "1111"
        },
        {
            "account" : "zxcv",
            "password" : "2222"
        },
        {
            "account" : "aaaa",
            "password" : "3333"
        }
    ]
    
}
```