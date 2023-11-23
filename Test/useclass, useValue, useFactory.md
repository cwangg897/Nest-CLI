### useclass
useClass를 사용하여 클래스를 재정의하면 새로운 인스턴스가 생성되어 해당 클래스의 생성자가 호출됩니다.
```ts
// AppModule에서 useClass를 사용하여 ExampleService를 재정의
@Module({
  providers: [
    {
      provide: ExampleService,
      useClass: CustomExampleService,
    },
  ],
})
export class AppModule {}

// CustomExampleService는 ExampleService를 확장하고 메시지를 재정의한 클래스
@Injectable()
export class CustomExampleService extends ExampleService {
  getMessage(): string {
    return 'Hello from CustomExampleService!';
  }
}

```

### useValue
useValue를 사용하여 프로바이더를 특정 값으로 설정할 수 있습니다.
ExampleService에 값은 = 이거를 쓰겠다 아는것을 명시하는것이었다
ts는 함수모임도 값으로 가능하니까
```ts
@Injectable()
export class ExampleService {
  getMessage(): string {
    return 'Hello from ExampleService!';
  }
}

// AppModule에서 useValue를 사용하여 ExampleService를 특정 값으로 재정의
@Module({
  providers: [
    {
      provide: ExampleService,
      useValue: {
        getMessage: () => 'Hello from useValue!',
      },
    },
  ],
})
export class AppModule {}
```

### useFactory
useFactory를 사용하여 특정 함수를 호출하여 프로바이더를 설정할 수 있습니다. <br>
useFactory는 오버라이드해서 사용하겠다 이런느낌  <br>
```ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class ExampleService {
  getMessage(): string {
    return 'Hello from ExampleService!';
  }
}

// Factory 함수. AppModule이 초기화될 때 실행된다.
const exampleServiceFactory = () => {
  return {
    getMessage: () => 'Hello from useFactory!',
  };
};

// AppModule에서 useFactory를 사용하여 ExampleService를 특정 함수로 재정의
@Module({
  providers: [
    {
      provide: ExampleService,
      useFactory: exampleServiceFactory,
    },
  ],
})
export class AppModule {}
```
```
위의 코드에서 exampleServiceFactory는 ExampleService를 반환하는 함수입니다.
이 함수는 모듈이 초기화될 때 한 번 실행됩니다. useFactory를 사용하여 프로바이더를 설정할 때, 반환된 객체가 해당 프로바이더로 사용됩니다.
이렇게 사용하면 useFactory 함수를 통해 프로바이더를 동적으로 생성할 수 있습니다.
이는 특정 조건에 따라 다른 객체를 반환하고 싶을 때, 또는 의존성 주입을 동적으로 처리하고 싶을 때 유용합니다.

```
