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

### 토큰으로 로그인하는 경우
```
1. 토큰으로 로그인한다면 토큰이 무사한지 verify
2. 토큰을 split하기
3. decode해서 거기서 accessd인지확인하기
```

```ts
    decodeBasicToken(base64String: string){
        const decoded = Buffer.from(base64String, 'base64').toString('utf8');

        const split = decoded.split(':');

        if (split.length !== 2) {
          throw new UnauthorizedException('잘못된 유형의 토큰입니다.');
        }
    
        const email = split[0];
        const password = split[1];

        return {
            email,
            password,
        }
    }
// verify는 누군지 이런게 안중요한게 어차피 토큰으로 자기꺼면 돌려주니까 남의것이면 남의거 돌려주니까
    verifyToken(token: string) {
        return this.jwtService.verify(token, {
            secret: JWT_SECRET,
        });
    }

// 토큰으로 로그인하는 경우 vefiry검증 payload를 반환한다
  async verify(token: string) {
    return this.jwtService.verify(token, {
      secret: JWT_SECRET,
    });
  }

```


### 토큰 갱신
```ts
    async rotateToken(token: string, isRefreshToken: boolean) {
        const decoded = this.jwtService.verify(token, {
            secret: JWT_SECRET,
        });

        if(decoded.type !== 'refresh'){
            throw new UnauthorizedException('토큰 재발급은 Refresh 토큰으로만 가능합니다!');
        }

        return this.signToken({
            ...decoded,
        }, isRefreshToken);
    }

```

### refereshToken이 만료되면 어찌할가
 access token을 검증하여 refresh token 재발급 <br>
`https://inpa.tistory.com/entry/WEB-📚-Access-Token-Refresh-Token-원리-feat-JWT [Inpa Dev 👨‍💻:티스토리]` <br>
