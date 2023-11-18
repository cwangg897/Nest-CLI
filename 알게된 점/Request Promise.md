### 문제
await req.user;에서 await를 안해줘서 오류가생겼다 ts에서 가장흔한 오류이다 <br>
이런거는 잘 확인해야겠다 <br>
```ts
export class RoleGuard implements CanActivate {
  constructor(
    private reflector: Reflector,
    private readonly authService: AuthService,
  ) {}
  async canActivate(context: ExecutionContext): Promise<boolean> {
    // HasRole로 넣은 메타데이터
    const requiredRoles = this.reflector.getAllAndOverride<UserRole[]>(
      ROLE_KEY,
      [context.getHandler(), context.getClass()],
    );
    /**
     * context에서 token에서 역할을 빼내야함
     *
     */
    const req = context.switchToHttp().getRequest();
    const user = await req.user;
    // role을 여러개 가질 수 있다면?...
    for (const role of requiredRoles) {
      if (role === UserRole.ALL) return true;
      if (user.role === role) return true;
    }
    return false;
  }
}

```
