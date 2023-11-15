
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
