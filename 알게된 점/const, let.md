### const
const는 상수를 선언하는 키워드로, 값을 한 번 할당하면 재할당할 수 없는 변수를 생성합니다.
선언과 동시에 값을 할당해야 합니다.
즉 다음코드에서 let인 부분을 const-> let로 변경하면서 const는 바로 값이 할당되어야한다는걸 알게도이ㅓㅆ다
```ts
    let category;
    let updateProduct;
    if (dto.categoryName) {
      category = await this.categoryRepository.findByName(dto.categoryName);
      if (!category) {
        throw new BadRequestException('존재하지 않는 카테고리입니다');
      }
      updateProduct = {
        ...product,
        ...dto,
        category,
      };
    } else {
      updateProduct = {
        ...product,
        ...dto,
      };
    }


```
