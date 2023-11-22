### Wiston을 활용하자
내장로깅과 커스텀에서 사용할 수 있다 <br>
내장은 DB로나 외부로 보낼 수 없기때문에 커스텀으로 주로 사용한다. <br>
그런데 커스톰보다 이미 만들어지고 상용화된 곳엔 winston을 주로사용한다. <br>


### 패키지 설치
```ts
$ pnpm add winston
$ pnpm add nest-winston

후에 모듈에 임포트
AppMoudle에 하는게 좋을듯 전역으로 사용하니까
```

### 로그를 내보내는법
```ts
        new winston.transports.File({
          filename: './kurkus.log', // 로그 파일 경로
          level: 'info', // 로그 레벨 (예: info, error, warn 등)
          format: winston.format.combine(
            winston.format.timestamp(),
            winston.format.json(),
          ),
        }),
```
끝나고 보니 생겨있다 이를통해서 ELK로 로그를 보내서 관리하는것도 좋은방법인것 같다 <br>
<img width="1475" alt="image" src="https://github.com/cwangg897/Nest-Record/assets/79621675/6bf24f1a-cc96-4db9-a22d-149327ca8ca1">
