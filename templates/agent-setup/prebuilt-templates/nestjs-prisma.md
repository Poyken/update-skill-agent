# 🟢 NestJS + Prisma Template

> Pre-built `.agent` template cho dự án NestJS với Prisma ORM, TypeScript, PostgreSQL và JWT Authentication.

---

## ⚡ Quick Setup

```bash
# 1. Tạo folder .agent
mkdir -p .agent/{memory,rules,workflows,checklists,skills}

# 2. Copy từng file bên dưới vào đúng vị trí
```

---

## 📁 FILE: `.agent/memory/project-context.md`

```markdown
# Project Memory - [PROJECT_NAME]

> Cập nhật: [DATE]

## Mô tả ngắn gọn

[Backend API cho ___]

## Tech Stack

| Layer          | Công nghệ                           |
| -------------- | ----------------------------------- |
| Framework      | NestJS 10                           |
| Language       | TypeScript (Strict mode)            |
| ORM            | Prisma                              |
| Database       | PostgreSQL 15                       |
| Authentication | JWT + Passport                      |
| Validation     | class-validator + class-transformer |
| Documentation  | Swagger/OpenAPI                     |
| Testing        | Jest                                |
| API Format     | RESTful                             |

## Cấu trúc thư mục
```

src/
├── modules/ # Feature modules
│ ├── auth/
│ │ ├── auth.controller.ts
│ │ ├── auth.service.ts
│ │ ├── auth.module.ts
│ │ ├── dto/
│ │ ├── guards/
│ │ └── strategies/
│ ├── users/
│ └── [other-modules]/
├── common/ # Shared code
│ ├── decorators/
│ ├── filters/
│ ├── guards/
│ ├── interceptors/
│ └── pipes/
├── config/ # Configuration
├── prisma/ # Prisma client
└── main.ts

prisma/
├── schema.prisma
└── migrations/

```

## Trạng thái hiện tại

- [x] Project setup (NestJS, Prisma, PostgreSQL)
- [x] Authentication (JWT)
- [x] Users CRUD
- [ ] [Module 1]
- [ ] [Module 2]

## 🔄 Đang làm dở

- **Feature:** [Current feature]
- **Branch:** feature/[branch-name]
- **Status:** [X]%

## 🐛 Bugs đã fix

### Bug #1: Prisma Connection Pool Exhausted
- **Triệu chứng:** Database connection timeout
- **Nguyên nhân:** Không dùng singleton PrismaService
- **Cách fix:** Extend PrismaService với onModuleInit/onModuleDestroy
- **Bài học:** Luôn dùng Prisma singleton pattern

## ⚠️ Quirks

- Prisma migrate cần `--create-only` trong production
- JWT secret phải ≥ 32 characters
- class-validator cần enableImplicitConversion trong ValidationPipe
```

---

## 📁 FILE: `.agent/rules/global.md`

```markdown
# Quy tắc Code Chung - [PROJECT_NAME]

> ⚠️ Các quy tắc này được rút ra từ code hiện có.

## 1. Naming Conventions

| Loại        | Pattern             | Evidence                              |
| ----------- | ------------------- | ------------------------------------- |
| Modules     | kebab-case folder   | `src/modules/user-profile/`           |
| Controllers | .controller.ts      | `src/modules/auth/auth.controller.ts` |
| Services    | .service.ts         | `src/modules/auth/auth.service.ts`    |
| DTOs        | PascalCase + Dto    | `CreateUserDto`, `UpdateUserDto`      |
| Entities    | PascalCase (Prisma) | Defined in `prisma/schema.prisma`     |
| Guards      | PascalCase + Guard  | `JwtAuthGuard`                        |

## 2. Module Structure
```

module-name/
├── module-name.controller.ts # HTTP handlers
├── module-name.service.ts # Business logic
├── module-name.module.ts # NestJS module
├── dto/
│ ├── create-[name].dto.ts
│ └── update-[name].dto.ts
├── entities/ # Response entities (Swagger)
│ └── [name].entity.ts
└── guards/ # Module-specific guards

````

## 3. Controller Pattern

```typescript
// từ src/modules/users/users.controller.ts
@Controller('users')
@ApiTags('users')
@UseGuards(JwtAuthGuard)
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  @ApiOperation({ summary: 'Get all users' })
  @ApiResponse({ status: 200, type: [UserEntity] })
  findAll() {
    return this.usersService.findAll();
  }

  @Get(':id')
  @ApiOperation({ summary: 'Get user by ID' })
  findOne(@Param('id') id: string) {
    return this.usersService.findOne(id);
  }

  @Post()
  @ApiOperation({ summary: 'Create user' })
  create(@Body() dto: CreateUserDto) {
    return this.usersService.create(dto);
  }
}
````

## 4. Service Pattern

```typescript
// từ src/modules/users/users.service.ts
@Injectable()
export class UsersService {
  constructor(private prisma: PrismaService) {}

  async findAll() {
    return this.prisma.user.findMany();
  }

  async findOne(id: string) {
    const user = await this.prisma.user.findUnique({ where: { id } });
    if (!user) {
      throw new NotFoundException(`User #${id} not found`);
    }
    return user;
  }

  async create(dto: CreateUserDto) {
    return this.prisma.user.create({ data: dto });
  }
}
```

## 5. DTO Pattern (class-validator)

```typescript
// từ src/modules/users/dto/create-user.dto.ts
import { IsEmail, IsString, MinLength, IsOptional } from "class-validator";
import { ApiProperty, ApiPropertyOptional } from "@nestjs/swagger";

export class CreateUserDto {
  @ApiProperty({ example: "john@example.com" })
  @IsEmail()
  email: string;

  @ApiProperty({ example: "John Doe" })
  @IsString()
  @MinLength(2)
  name: string;

  @ApiPropertyOptional()
  @IsOptional()
  @IsString()
  avatar?: string;
}
```

## 6. Error Handling

```typescript
// Dùng NestJS built-in exceptions
throw new NotFoundException("Resource not found");
throw new BadRequestException("Invalid input");
throw new UnauthorizedException("Not authenticated");
throw new ForbiddenException("Not authorized");

// Custom exception filter trong src/common/filters/
@Catch()
export class AllExceptionsFilter implements ExceptionFilter {
  catch(exception: unknown, host: ArgumentsHost) {
    // ...
  }
}
```

## 7. Prisma Usage

```typescript
// Singleton pattern - từ src/prisma/prisma.service.ts
@Injectable()
export class PrismaService extends PrismaClient implements OnModuleInit, OnModuleDestroy {
  async onModuleInit() {
    await this.$connect();
  }

  async onModuleDestroy() {
    await this.$disconnect();
  }
}

// Transactions
await this.prisma.$transaction(async (tx) => {
  await tx.order.create({ data: orderData });
  await tx.inventory.update({ ... });
});
```

## 8. Authentication

```typescript
// JWT Guard usage
@UseGuards(JwtAuthGuard)
@Get('profile')
getProfile(@Request() req) {
  return req.user;
}

// Get current user
@Get('me')
getMe(@CurrentUser() user: User) {
  return user;
}
```

````

---

## 📁 FILE: `.agent/workflows/create-new-feature.md`

```markdown
# Workflow: Tạo Module Mới

## Bước 1: Tạo branch

```bash
git checkout develop
git pull origin develop
git checkout -b feature/[module-name]
````

## Bước 2: Tạo Prisma model (nếu cần)

```prisma
// prisma/schema.prisma
model [ModelName] {
  id        String   @id @default(cuid())
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  // fields...
}
```

```bash
npx prisma migrate dev --name add_[model]
npx prisma generate
```

## Bước 3: Generate NestJS module

```bash
nest g module modules/[module-name]
nest g controller modules/[module-name]
nest g service modules/[module-name]
```

## Bước 4: Tạo DTOs

```bash
mkdir src/modules/[module-name]/dto
touch src/modules/[module-name]/dto/create-[name].dto.ts
touch src/modules/[module-name]/dto/update-[name].dto.ts
```

```typescript
// create-[name].dto.ts
import { IsString, IsNotEmpty } from 'class-validator';
import { ApiProperty } from '@nestjs/swagger';

export class Create[Name]Dto {
  @ApiProperty()
  @IsString()
  @IsNotEmpty()
  field: string;
}
```

## Bước 5: Implement Service

```typescript
@Injectable()
export class [Name]Service {
  constructor(private prisma: PrismaService) {}

  findAll() { return this.prisma.[model].findMany(); }
  findOne(id: string) { return this.prisma.[model].findUnique({ where: { id } }); }
  create(dto: Create[Name]Dto) { return this.prisma.[model].create({ data: dto }); }
  update(id: string, dto: Update[Name]Dto) { return this.prisma.[model].update({ where: { id }, data: dto }); }
  remove(id: string) { return this.prisma.[model].delete({ where: { id } }); }
}
```

## Bước 6: Implement Controller

```typescript
@Controller('[module-name]')
@ApiTags('[module-name]')
@UseGuards(JwtAuthGuard)
export class [Name]Controller {
  constructor(private readonly service: [Name]Service) {}

  @Get()
  findAll() { return this.service.findAll(); }

  @Get(':id')
  findOne(@Param('id') id: string) { return this.service.findOne(id); }

  @Post()
  create(@Body() dto: Create[Name]Dto) { return this.service.create(dto); }

  @Patch(':id')
  update(@Param('id') id: string, @Body() dto: Update[Name]Dto) { return this.service.update(id, dto); }

  @Delete(':id')
  remove(@Param('id') id: string) { return this.service.remove(id); }
}
```

## Bước 7: Register module

```typescript
// src/app.module.ts
@Module({
  imports: [
    // ...
    [Name]Module,
  ],
})
export class AppModule {}
```

## Bước 8: Test

```bash
npm run test -- src/modules/[module-name]
npm run test:e2e -- [module-name]
```

## Bước 9: Commit

```bash
git add .
git commit -m "feat([module-name]): implement [module-name] CRUD

- Add Prisma model
- Add DTOs with validation
- Add service with CRUD operations
- Add controller with Swagger docs
- Add tests"

git push origin feature/[module-name]
```

````

---

## 📁 FILE: `.agent/checklists/pr-review.md`

```markdown
# PR Review Checklist - NestJS

## Database
- [ ] Prisma migration created
- [ ] Migration có thể rollback
- [ ] Indexes cho frequently queried fields
- [ ] Không có N+1 queries

## API Design
- [ ] RESTful endpoints
- [ ] Proper HTTP status codes
- [ ] Swagger decorators đầy đủ
- [ ] Request/Response DTOs

## Validation
- [ ] Input validation với class-validator
- [ ] Custom validators cho business rules
- [ ] Error messages rõ ràng

## Authentication/Authorization
- [ ] Protected routes có guards
- [ ] Role-based access nếu cần
- [ ] Sensitive data không exposed

## Error Handling
- [ ] Proper exception types
- [ ] No sensitive info in errors
- [ ] Logging cho errors

## Testing
- [ ] Unit tests cho service
- [ ] E2E tests cho controller
- [ ] Coverage ≥ 80%
````

---

## 🎯 Sau khi copy

Chạy prompt này để customize:

```
Tôi đã copy NestJS + Prisma template vào .agent/

Hãy đọc các files và CUSTOMIZE cho dự án hiện tại:
1. Đọc prisma/schema.prisma để biết models
2. Quét src/modules/ để cập nhật structure
3. Tìm 3 modules thực tế làm evidence
4. Cập nhật trạng thái dựa trên code hiện có

Output từng file đã customized.
```

---

**← Quay lại:** [Pre-built Templates](./README.md)
