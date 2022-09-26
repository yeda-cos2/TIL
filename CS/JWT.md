## 인증 / 인가
인증: 등록된 사용자인지 확인하는 것<br>
인가: 인증된 사용자가 권한이 있는지 확인하는 것<br><br>

## Http 통신
Http 통신은 stateless하다. 요청에 대한 응답을 하면 그걸로 끝이다! <br>
응답 후의 상태를 저장하지 않기 때문에, 요청에 대해 <br>
1)인증된 사용자인지 <br>
2)사용자가 해당 요청에 대한 권한이 있는지 확인해야 한다.<br>
이를 위한 방법으로 JWT를 많이 채택하고 있다.<br><br>

## JWT(Json Web Token)
### JWT의 구조<br>
![다운로드](https://user-images.githubusercontent.com/97859770/192280057-5049b958-b778-4f20-80c3-ade8c35efbf5.jpg)

<b>Header</b> <br>
헤더에는 typ(타입), alg(해싱 알고리즘) 두 가지 정보가 담긴다. 타입은 토큰 타입으로 JWT를 의미하고, 해싱 알고리즘은 토큰을 검증할 때 사용되는 signature에서 사용된다.<br>
```
{
  "typ": "JWT",
  "alg": "HS256"
}
```
<br>

<b>Payload</b> <br>
페이로드에는 토큰에 담을 정보가 들어간다. 이때 정보의 한 조각을 클레임이라고 하는데, payload에 여러 개의 클레임을 넣을 수 있다.
클레임은 key, value의 JSON 데이터 한 쌍으로 이루어진다.
<br><br><br>

<b>Signature</b> <br>
header, payload을 인코딩하여 합친 후 비밀키로 해쉬하여 생성한 값이다.<br>

```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
  ```
<br>

Base64로 인코딩하고 => header의 alg 기법으로 해쉬하고 => 이 값을 다시 Base64로 인코딩 한 값이 signature에 담긴다.<br><br>

## JWT를 신뢰할 수 있는 이유
누구나 JWT가 있으면 쉽게 payload에 담긴 값을 확인할 수 있다.<br>
header와 payload에 담긴 정보는 단순히 Base64로 '인코딩' 되어있기 때문에 디코딩만 거치면 된다.<br><br>

❓ 이렇게 누구나 볼 수 있는 정보를 어떻게 신뢰하나?<br>
signature 때문에 신뢰할 수 있다! signature에는 header, payload를 인코딩한 값을 해싱한 값이 담긴다.<br>
해쉬를 통해 해당 값이 변조되지 않은 값(무결성)임을 확인할 수 있고, 신뢰할 수 있다.<br><br>
 
