### 문제상황
finallly를사용하면 return을 해도 항상 동작한다  <br>
그런데 문제점은 예외를 터뜨려서 예외메시지를 봐야하지만 finally가 동작해서 아래 사진과같이 응답하게 된다. <br>
![image](https://github.com/cwangg897/Nest-Record/assets/79621675/571e31f6-d5f0-4cf3-9349-57fd587b9445)


### 해결방법
띠용 throw하면되는데 이거를 핸들링할게 필요한거 같다 전역예외 핸들러가 필요하다
```ts
      const newOrder = await queryRunner.manager.save(Order, orderEntity);
      await queryRunner.commitTransaction();
      return newOrder;
    } catch (err) {
      await queryRunner.rollbackTransaction();
      throw err;
    } finally {
      await queryRunner.release();
    }
```
