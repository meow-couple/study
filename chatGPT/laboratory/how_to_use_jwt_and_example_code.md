

```java
import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;

import java.util.Date;

public class JwtExample {

    private static final String SECRET_KEY = "mysecretkey";

    public static void main(String[] args) {

        // Define the payload
        String user_id = "12345";
        String email = "user@example.com";

        // Generate a token
        String token = Jwts.builder()
                .claim("user_id", user_id)
                .claim("email", email)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 3600000))
                .signWith(SignatureAlgorithm.HS256, SECRET_KEY)
                .compact();

        // Decode the token
        Claims claims = Jwts.parser()
                .setSigningKey(SECRET_KEY)
                .parseClaimsJws(token)
                .getBody();

        // Extract information from the decoded token
        user_id = claims.get("user_id", String.class);
        email = claims.get("email", String.class);
    }
}
```

이 예제에서는 먼저 `io.jsonwebtoken` 패키지에서 필요한 클래스를 가져옵니다. 페이로드는 `user_id`와 `email` 문자열을 만들어 정의합니다. 그런 다음, 페이로드와 비밀 키를 전달하여 `Jwts.builder()` 메소드를 사용하여 토큰을 생성합니다. 토큰의 만료 시간과 서명 알고리즘도 지정합니다.

우리는 `Jwts.parser()` 메소드를 사용하여 비밀 키를 전달하여 토큰을 디코딩합니다. 그런 다음 `Claims` 객체를 사용하여 디코딩된 토큰에서 `user_id` 및 `email` 값을 추출합니다.

비밀 키는 페이로드의 정보에 액세스하지 않아야 하는 사람과 공유하지 말아야하므로 비밀로 유지해야합니다.