# [HTTP] Get 요청시 Body를 포함할 수 있을까?

[HTTP/1.1 및 HTTP/2의 표준 명세 (RFC 7231)](https://developer.mozilla.org/ko/docs/Web/HTTP/Reference/Methods/GET) 에 따르면 GET 요청은 Body를 포함하지 않는 것을 **권장**함.

- GET은 리소스를 요청하는 목적이므로 서버가 Body를 해석하지 않는 것이 기본 동작임.
- 다만, HTTP 명세에서 GET 요청의 Body를 완전히 금지하지는 않음. 가능은 함.

<aside>
💡

Body를 포함하는 GET 요청은 가능하지만, 대부분의 서버와 클라이언트 라이브러리가 이를 허용하지 않고 있음.

</aside>

### In Swift

실제로 `Moya`에서는 해당 케이스를 허용하지 않음.

```swift
// Moya 라이브러리를 사용해서 Body를 담아서 GET 요청을 한 경우 발생하는 에러
underlying(Alamofire.AFError.urlRequestValidationFailed(reason: Alamofire.AFError.URLRequestValidationFailureReason.bodyDataInGETRequest(21 bytes)), nil)
```

## GET 요청에서 Body를 사용하지 않도록 권장하는 이유

1. 캐시 가능성
    - HTTP GET 요청은 종종 웹 브라우저에 의해 캐시됨.
    - GET 요청을 간단하고 예측 가능하게 유지함으로써, 이러한 시스템이 캐시를 보다 쉽게 관리하고 검색할 수 있음.
2. 안전성
    - GET 요청은 "안전(safe)" 및 "멱등(idempotent)"이어야 합니다. 이것은 서버에서 어떠한 데이터도 수정하지 않고 부작용이 없어야 함을 의미함.
    - GET 요청에서 메시지 바디를 허용하지 않음으로써, GET 요청이 안전하고 멱등하게 유지되도록 보장함.
3. 보안성
    - GET 요청은 종종 서버 로그, 브라우저 히스토리 및 다른 시스템에서 기록함.
    - 데이터를 URL에 유지함으로써, 이를 쉽게 볼 수 있으며, 제3자에게 잠재적으로 가로챌 수 있음.
    - 반면, 메시지 바디에 데이터를 포함하는 POST 요청은 덜 가시적이며, 추가적인 보안 계층을 제공할 수 있음.
