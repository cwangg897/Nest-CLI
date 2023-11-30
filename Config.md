### DB정보라던지 숨겨야하는 정보를 관리하는파일
사용하는 방법은 root경로에 .env로하는데 개발환경과 production환경이 있다면은 <br>
production.env | dev.env를 하면된다. <br>

### 사용방법
`pnpm add @nestjs/config`를 하면 node에서 직접다루는것이아닌 더 편하게 다룰 수 있다

```ts
imports: [
    UsersModule,
    EmailModule,
    ConfigModule.forRoot({
      envFilePath:
        process.env.NODE_ENV === 'production'
          ? '.production.env'
          : process.env.NODE_ENV === 'dev'
            ? '.dev.env'
            : '.starge.env',
    }),
  ],
```


### 설정 방법
app.module.ts에 `ConfigModule.forRoot({ envFilePath: '.env', isGlobal: true})` 을 추가한다
isGlobal이란 다른곳에서 사용하려면 모두 import를 넣어줘야하는데 그럴필요가없는경우
그리고 ConfigService를 사용하면 된다
```ts
  constructor(
    private readonly memberService: MemberService,
    private readonly jwtService: JwtService,
    private readonly configService: ConfigService,
  ) {}

아래와 같이 사용하기
this.configService.get<number>('HASH_ROUNDS') // 싱글 쿼트로 넣어주다가 오타생기면 문제생기고 value가 변경되면 문제생김 그래서 key값을저장하는 파일을 따로 만듬
개선하기
common에 const폴더안에 값을 미리 만들어두기
this.configService.get<number>('HASH_ROUNDS')
```
#### app module에서 사용하는법
app모듈은 ConfigService를 바로사용하지못한다 모듈을 구성하는 환경이니까 그래서 process를이용한다. <br>
env는 map이라고생각 <br>
process는 global변수이다 <br>
```ts
    TypeOrmModule.forRoot({
      type: 'mysql',
      host: process.env[ENV_DB_HOST_KEY],
      port: parseInt(process.env[ENV_DB_PORT_KEY]),
      username: process.env[ENV_DB_USERNAME_KEY],
      password: process.env[ENV_DB_PASSWORD_KEY],
      database: 'board',
      entities: [Member, Board],
      synchronize: true,
    }),
```

### process db type오류
```
type 속성에 process.env[ENV_DB_DATABASE_KEY]를 사용하는 경우, 여러 가지 문제가 발생할 수 있습니다. 
주요 이슈 중 하나는 process.env[ENV_DB_DATABASE_KEY]가 undefined일 수 있고, 이로 인해 데이터베이스 연결 설정이 올바르게 이루어지지 않을 수 있습니다.
```


### dotenv
패키지 @nestjs/config는 내부적으로 dotenv 를 사용합니다 .
dotenv는 환경변수를 . env파일에 저장하고 process.env로 로드하는 모듈이다





### 다른파일을 만들어서 주입하는경우 (Load)
```ts
import configuration from './config/configuration';

@Module({
  imports: [
    ConfigModule.forRoot({
      load: [configuration],
    }),
  ],
})
export class AppModule {}
```


### 노드에서 환경변수 바꾸는법
`NODE_ENV=development nest start --watch`을 package.json에 넣어두면 매번 명령어를 바꾸지않아도 된다.


### 궁금
예를 들어, emailConfig는 load 배열에 포함된 설정 로더로 가정하겠습니다. <br>
이 설정 로더는 이메일 관련 설정을 반환하는 함수 또는 클래스 일 것입니다. <br> ConfigModule.forRoot()는 이러한 설정 로더들을 실행하고 반환된 설정을 모두 합쳐 최종적인 설정 객체를 만듭니다.

```ts
ConfigModule.forRoot({
  envFilePath:
    process.env.NODE_ENV === 'production'
      ? '.production.env'
      : process.env.NODE_ENV === 'dev'
        ? '.dev.env'
        : '.starge.env',
  load: [emailConfig]
}),
```
위의 코드에서는 emailConfig가 설정 로더로 사용되고, ConfigModule는 emailConfig에서 반환된 설정과 환경 파일에서 읽은 설정을 합쳐 최종적인 설정 객체를 생성합니다. <br> 이를 통해 여러 소스에서 가져온 설정들을 효과적으로 관리할 수 있습니다.
