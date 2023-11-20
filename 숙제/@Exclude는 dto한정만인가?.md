### 설명
다음코드에서 ...dto에서 categoryName을 빼고싶다 왜냐하면 저거는 공통된 값이 아니기 때문이다 <br>
나머지는 공통되기때문에 ...dto로 하는데 반환된 타입은 any이다 그래서 추측은 dto에 exclude를 걸면은 <br> 
response할때도 그 타입이면 모르지만 그 타입이 아니라면 exclude가 걸리지 않는다는 점이다. <br>
```ts
  async updateProduct(dto: UpdateProductDto, id: number) {
    // update는 product를가져와서 대체해서 save시킴
    const product = await this.productRepository.findById(id);
    if (!product) {
      throw new BadRequestException('존재하지 않는 상품입니다');
    }
    //product에서 함께들고온 category를 업데이트해서 넣으면 안되는것인가?

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
    delete updateProduct.categoryName;
    // 당연히 그대로니까 변경이 안먹힘
    return this.productRepository.update(updateProduct);
  }

```


### 해결방법
그래서 해결방법은 delete를 사용하는것인데 더 좋은방법이 있는지는 공부하면서 알게될것 같다. 
