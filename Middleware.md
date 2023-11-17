### 미들웨어
미들웨어는 라우트 핸들러 이전에 호출되는 함수입니다.
미들웨어 기능은 요청 및 응답 개체에 액세스할 수 있다.


### 간단 작성방법
```ts
@Injectable()
export class LogMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log(req.url);
  }
}
```
