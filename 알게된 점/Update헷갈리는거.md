Product이니까 이렇게 업데이트하는게 제일 최고 <br>

```ts
const updateProduct = {
  ...product,
  ...dto,
  category: {
    ...product.category, // 기존 카테고리 속성을 그대로 유지
    // 추가적인 업데이트가 필요한 경우, 여기에 업데이트할 속성을 추가
  },
};
```
