### 헤더를 조작하는 방법
책에서는 헤더에 값을 추가하는 방법을 다음과 같이 진행했다 그런데 나는 저러면 값을 조작하지 못한다고 생각했다.
그래서 생각한게 직접 Response객체를 조작하는것이다
```ts
  @Header('customeheader', 'head')
  @Get('test')
  testHandler() {
    return 'hello test';
  }
```

오류는 요청을 하면 응답을 못받는것이다. 생각해보니까 status를 주지않고 값도 주지않기때문에 요청만 계속하고 기다리는 것이었다
```ts
  @Get('test')
  testHandler(@Response() res) {
    // 특정 헤더 추가
    res.header('Custom', 'YourCustomValue');

    // 상태 코드 설정
    res.status(202).send('Response with custom header');
  }
```

```ts

  @Get('test')
  testHandler(@Response() res) {
    res.header('customheader', 2);
    return res.status(202).send('hello test');
    // res.status(202).send('hello test');
  }
```
수정코드 간단한것인데 왜 이런생각을 못했을가..
