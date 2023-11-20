### TypeORM의 soft delete
타입 orm의 soft delete는 엄청편하다 <br>
왜냐하면 따로 어떠한 작업도 안해줘도 된다. 더해서 JPA에는 있는지 잘 모르지만 쿼리에서도 자동으로 제외를 시켜주는것이다. <br>
일단은 전용 컬럼을 제공해준다는거 자체가 편리하다고 생각한다. <br>
쿼리빌더에서도 제외시켜주는 메소드 체이닝을 제공한다 

### 사용방법
```ts
  @DeleteDateColumn({ name: 'deleted_at', type: 'timestamp', nullable: true })
  deletedAt: Date;
```
다음 코드를 추가해줍니다. 

