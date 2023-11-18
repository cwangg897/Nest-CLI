### 설정
`pnpm add typeorm @nestjs/typeorm mysql2  `

### TypeOrmModule - Appmoudle  
ENV를 통해서 관리하기
```ts
TypeOrmModule.forRoot({
      type: 'postgres',
      host: process.env[ENV_DB_HOST_KEY] || 'localhost',
      port: parseInt(process.env[ENV_DB_PORT_KEY]) || 5433,
      username: process.env[ENV_DB_USERNAME_KEY] || 'postgres',
      password: process.env[ENV_DB_PASSWORD_KEY] || 'postgres',
      database: process.env[ENV_DB_DATABASE_KEY] || 'postgres',
      entities: [PostsModel, UsersModel, ImageModel, MessagesModel, ChatsModel],
      synchronize: true,
    })
```
