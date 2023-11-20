### Pick
Pick을 활용하면 타입을 뽑아 올 수 있었다 <br>
Pick, Omit, Partial <br>

### 상속
타입스크립트에서 상속은 타입이 아니라 값이 필요하다 <br>
그래서 값을 반환해주는 PickType을 사용해야한다. <br>
Type이 붙어있어야 값을 반환한다


### Omit 타입스크립트의 진실
```ts
  async create(
    dto: Omit<CreateProductDto, 'categoryName'>,
    category: Category,
  ) {
    const product = this.productRepository.create({
      ...dto,
      category,
    });
    return this.productRepository.save(product);
  }
```
에서 발견한 사실은 타입으로 코드에서만 dto.categoryName을 못사용하는거지 
디버깅을 찍어보니 dto내부에는 값이 존재한다.
<img width="1086" alt="image" src="https://github.com/cwangg897/Nest-Record/assets/79621675/8dcce027-9388-498f-be86-84feb306790e">
