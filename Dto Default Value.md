### 문제상황
dto에도 default값을 넣어주고싶다. 그런데 param같은경우는 = 으로 할당가능하지만 <br>
dto class에 default값을 넣어주고싶다면은 그냥은 동작을 안한다. <br>
```ts
  @IsIn(['ASC']) // 무조건 ASC만 들어와야 리스트에있는 값만 허용하는것이다
  @IsOptional()
  order_createdAt?: string = 'ASC';
```

### 해결방법
main.ts에 다음코드를 추가해줍니다. <br>
파이프에서 변환을 해도된다는 것이다. <br>
```ts
  app.useGlobalPipes(
    new ValidationPipe({
      transform: true,
    }),
  );
```

### 쿼리파라미터 문제 dto - 해결방법 1
쿼리파라미터를 dto로 바꿀수있는데 쿼리파라미터는 string이다  <br>
그래서 다음과 같이 변환 시켜줘야한다 <br>
```ts
  @Type(() => Number)
  @IsNumber()
  @IsOptional()
  where__id_more_than?: number;
```
그런데 유용하지만 잘 사용하지 않는다 <br>

### 쿼리파라미터 문제 dto - 해결방법 2
```
main.ts에가서 enableImplicitConversion을 추가하면은 임의변화를 추가하는것이다.
이거를 넣어주면 default값만 넣어주는게 아니고 validator를 보고 숫자면은 숫자로되어있어야 정상이구나 자동으로 인지하고
자동으로 변화하고 validator 에노테이션을 통과 시킴 
정리하면 @Type(()=> Number) 를 생략하고 어노테이션에 입력된 타입기준으로 값을 변환시켜준다 (타입변환)
```

```ts
  app.useGlobalPipes(
    new ValidationPipe({
      transform: true,
      transformOptions: { enableImplicitConversion: true }, // 임의 변화를 허가한다
    }),
  );
```
