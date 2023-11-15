
<https://www.npmjs.com/package/class-validator>
```
pnpm add class-validator
```
```
class형식 dto들을 valid할 때 사용한다


```



### 추천하는 패턴
```
PickType을 사용하는것을 추천하는것이다. 
왜냐하면 Entity에 넣기전에 어차피 dto로 들어하는데 이 조건을 만족해야 하기때문에 Entity에 Validator를 걸어두면은 자동으로 적용이되고 PickType상속을 사용하면
되기때문이다.
단 스웨거 적으로는 동작을 못하게만드니 조금은 힘들거같다? 아니다 스웨거로 상속이되니 지장없을거같다
```


### Pipe와 class-validator
```
nsetjs의 class-validator를사용하면 pipe를 사용안해도되는데 class-validator는 어떻게 구현이 된건가요?

ChatGPT
NestJS에서 class-validator를 사용하면 파이프(pipe)를 직접 사용하지 않아도 됩니다. NestJS에서 class-validator는 미들웨어의 일부로 자동으로 적용됩니다. 이는 기본적으로 ValidationPipe라는 내장 파이프를 사용하여 이루어집니다.
```
