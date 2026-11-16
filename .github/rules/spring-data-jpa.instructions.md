---
description: Spring Data JPA, entity and persistence rules.
applyTo: '**/*Repository.java,**/*Entity.java,**/entity/**/*.java,**/domain/**/*.java,src/main/resources/db/**'
---

## Repositories
- Extend the narrowest Spring Data interface needed (`JpaRepository`, `CrudRepository`, or a custom read-only interface).
- Use derived query methods for simple lookups; use `@Query` for anything with more than two conditions.
- Always bind parameters (`:name` with `@Param`, or positional); never concatenate strings into JPQL, HQL or native SQL.
- Return `Optional<T>` for single results and `Page`/`Slice` for large collections; never return `null`.
- Use projections (interfaces or records) when the full entity is not needed.

## Entities
- Annotate with `@Entity` and an explicit `@Table(name = ...)`; use `jakarta.persistence` on Boot 3+.
- Use a surrogate `@Id` with an explicit generation strategy (`IDENTITY` or `SEQUENCE`).
- Provide a protected no-arg constructor and a constructor or factory for required fields.
- Do not use Lombok `@Data`, `@EqualsAndHashCode` or `@ToString` on entities; implement `equals`/`hashCode` on the identifier or a business key.
- Keep entities free of Jackson annotations and web concerns.
- Use `@Version` for optimistic locking on aggregates edited concurrently.
- Map enums with `@Enumerated(EnumType.STRING)`, never ordinal.
- Keep bidirectional associations in sync through helper methods on the owning aggregate.

## Fetching and performance
- Mark associations `FetchType.LAZY`; never use `FetchType.EAGER` on collections.
- Avoid N+1 queries: use `@EntityGraph` or `JOIN FETCH` for known access paths.
- Do not rely on open-session-in-view; set `spring.jpa.open-in-view=false` and map to DTOs inside the service transaction.
- Use batch operations (`saveAll`, `@Modifying` queries) for bulk writes; clear the persistence context in large batches.
- Add database indexes for every column used in a frequent filter, join or sort.

## Schema management
- Manage schema changes with Flyway or Liquibase migrations; migrations are append-only and never edited once applied.
- Do not use `spring.jpa.hibernate.ddl-auto` values `create`, `create-drop` or `update` outside local development and tests; use `validate` or `none`.
- Never put credentials in datasource URLs or properties files; supply them through the environment or a secrets manager.
