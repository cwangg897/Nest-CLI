### 사용방법
다음과 같이 UseInterceptor어노테이션을 달아주면 된다. <br>
@Exclude()를 달아준곳을 제외시킨다. 기본옵션으로는 요청과 응답시에 모두 제외시켜버리는것이다. <br>
```ts
  @Get(':id')
  @UseInterceptors(ClassSerializerInterceptor)
  getBoard(@Param('id', ParseIntPipe) id: number) {
    return this.boardService.getBoard(id);
  }
```

```ts
  @Column()
  @Exclude({
    toPlainOnly: true,
  })
```

### @Exclude()옵션
```
front(json plain object, )  -> backend  (class instance dto)  
toClassOnly : class instance로 변환될 때 사용
toPlainOnly : json으로 변환될 때만 사용
```

### api마다 사용하는것은 비효율적 문제 개선방법
```
모든 api에 적용되도록 하고싶다면 
app.module파일에가서   providers: [AppService, { provide: APP_INTERCEPTOR, useClass: ClassSerializerInterceptor }], 으로 바꾼다 
APP모듈은 전체적으로 실행하는것인데 전역적으로 적용하고싶다면 이렇게해야한다 
```

### @Expose
expose를 사용하면 호출시 같이 불러주는 역할을 하는거 같다
entity를 반환하면 그 타입이면   @Expose메소드가 작동하는거같다

