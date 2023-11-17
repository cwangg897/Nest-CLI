### 생성자기반 주입
생성자기반주입은 상속관계에있지 않는 경우 사용하는것이 좋다


### 속성기반 주입
속성기반주입은 상속관계에 있는경우 사용하는게 좋다
```ts
@Inject(ServiceA) private readonly serviceA: ServiceA;
```
