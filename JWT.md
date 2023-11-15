```
pnpm add @nestjs/jwt bcrypt
```


```
bcrypt사용시 추가해줄것
import * as bcrypt from 'bcrypt';
```

### JWT토큰으로 생성
```ts
핵심코드 payload를 JWT로 만들어준다
        return this.jwtService.sign(payload, {
            secret: JWT_SECRET,
            // seconds
            expiresIn: isRefreshToken ? 3600 : 300,
        });
```
