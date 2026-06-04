---
name: create a shared library
description: Use when creating the contract layer for a new feature — the starting point before API or Angular code. Contains DTOs, endpoint interfaces, enums, and error codes. Pure TypeScript only, no framework dependencies. Both backend and frontend import from it.
---

A shared library is the **contract layer** between API and all clients (web, CMS, mobile, E2E). It contains no Angular, no NestJS — pure TypeScript only. Every feature starts here.

## Where it lives
`libs/{feature-name}-shared/src/lib/`

## Folder structure

```
src/
  lib/
    endpoints/
      {feature}.endpoint.ts        ← interface + request/response classes + URL paths enum
    dto/
      {feature}.dto.ts
    error-codes/
      {feature}.error-codes.ts     ← error code enum (strings, not numbers)
    models/
      {feature}-status.ts          ← enums, constants, plain models
    commands/
      {feature}.command.ts         ← CQRS commands
    events/
      {feature}.api-events.ts
    i18n/
      {feature}-en.i18n.ts
  index.ts                         ← barrel export of everything
```

## Endpoint file pattern

```typescript
// 1. URL paths as enum
export enum ExampleEndpointPaths {
    list    = '/example/list',
    getById = '/example/getById',
    create  = '/example/create',
    update  = '/example/update',
    delete  = '/example/delete',
}

// 2. Endpoint interface
export interface ExampleEndpoint {
    list(request: ExampleListRequest, ...args: unknown[]): Promise<ExampleListResponse> | Observable<ExampleListResponse>;
    getById(request: ExampleGetByIdRequest, ...args: unknown[]): Promise<ExampleDto> | Observable<ExampleDto>;
    create(request: ExampleCreateRequest, ...args: unknown[]): Promise<ExampleDto> | Observable<ExampleDto>;
    update(request: ExampleUpdateRequest, ...args: unknown[]): Promise<ExampleDto> | Observable<ExampleDto>;
    delete(request: ExampleDeleteRequest, ...args: unknown[]): Promise<void> | Observable<void>;
}

// 3. Request/Response classes
export class ExampleListRequest {
    @ApiModelProperty({ required: false })
    @IsOptional()
    @IsNumber()
    page?: number;
}

export class ExampleListResponse {
    @ApiModelProperty({ type: () => ExampleDto, isArray: true })
    @ValidateNested({ each: true })
    @Type(() => ExampleDto)
    items: ExampleDto[];

    @ApiModelProperty()
    @IsNumber()
    total: number;
}
```

## Error codes pattern

```typescript
export enum ExampleErrorCodes {
    ExampleNotFound        = 'ExampleNotFound',
    ExampleAlreadyExists   = 'ExampleAlreadyExists',
    ExampleAccessDenied    = 'ExampleAccessDenied',
}
```

## Rules
- All request/response classes use `@ApiModelProperty()` + `class-validator` decorators together
- Use `@ValidateNested()` + `@Type(() => NestedClass)` for nested objects
- `void` responses are typed as `Promise<void> | Observable<void>` in the interface
- Endpoint paths start with the feature name prefix: `/example/...`
- Error code names are PascalCase strings matching the enum key
- No Angular imports, no NestJS imports — pure TypeScript + class-validator + class-transformer only
