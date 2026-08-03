# Anotações — Dependências Spring Boot

> Projeto: Sistema de Aprovação de Solicitação de Compra (Workflow Engine)
> Stack: Vue 3 + TS (front) | Spring Boot + JPA (back) | PostgreSQL (banco)

---

## 1. Essenciais (marcar no Spring Initializr)

### Spring Web
- **O que é:** framework pra criar aplicações web e REST APIs.
- **Pra que serve aqui:** criar os `Controllers` (`/purchase-requests`, `/approvals`, etc).
- **Pacote:** `org.springframework.boot:spring-boot-starter-web`

### Spring Data JPA
- **O que é:** abstração sobre JPA/Hibernate pra facilitar acesso a dados.
- **Pra que serve aqui:** mapear as entidades (`PurchaseRequest`, `ApprovalStep`, `User`) e criar repositórios sem escrever SQL na mão.
- **Pacote:** `org.springframework.boot:spring-boot-starter-data-jpa`
- **Conceitos-chave:** `@Entity`, `@Repository`, `JpaRepository<T, ID>`

### PostgreSQL Driver
- **O que é:** driver JDBC específico pro PostgreSQL.
- **Pra que serve aqui:** permitir que o Spring converse com o banco Postgres rodando no Docker.
- **Pacote:** `org.postgresql:postgresql`
- **Nota:** já mexi nisso no `spring-boot-study-jpa` — cuidado com o nome da classe do driver no `application.properties`/`application.yml`.

### Validation
- **O que é:** implementação do Bean Validation (Jakarta Validation).
- **Pra que serve aqui:** validar campos de entrada, tipo `@NotNull` no `amount`, `@Email` no `User`, `@Positive` em valores monetários.
- **Pacote:** `org.springframework.boot:spring-boot-starter-validation`
- **Conceitos-chave:** `@Valid` no Controller, anotações nas entidades/DTOs.

### Lombok
- **O que é:** biblioteca que gera código repetitivo via anotações (getters, setters, construtores).
- **Pra que serve aqui:** evitar boilerplate nas entidades e DTOs.
- **Pacote:** `org.projectlombok:lombok`
- **Conceitos-chave:** `@Data`, `@Builder`, `@NoArgsConstructor`, `@AllArgsConstructor`
- **Nota:** precisa do plugin do Lombok na IDE pra funcionar direito (autocomplete etc).

---

## 2. Autenticação e Autorização

> Deixar pra depois que o fluxo de aprovação já estiver funcionando com usuário "fake"/hardcoded.

### Spring Security
- **O que é:** framework de segurança do Spring (autenticação + autorização).
- **Pra que serve aqui:** controlar quem pode aprovar em cada nível (`MANAGER`, `DIRECTOR`, `FINANCE`).
- **Pacote:** `org.springframework.boot:spring-boot-starter-security`

### JWT (jjwt)
- **O que é:** biblioteca pra gerar/validar tokens JWT (não vem no Initializr, adicionar manualmente).
- **Pra que serve aqui:** autenticação stateless, com o `role` do usuário embutido no token.
- **Pacote:** `io.jsonwebtoken:jjwt-api` (+ `jjwt-impl` e `jjwt-jackson` em runtime)

---

## 3. Qualidade / Organização (recomendado, não bloqueia o MVP)

### Spring Boot DevTools
- **O que é:** ferramentas de produtividade pra desenvolvimento (hot reload).
- **Pra que serve aqui:** não precisar reiniciar a aplicação a cada mudança de código.
- **Pacote:** `org.springframework.boot:spring-boot-devtools`

### MapStruct
- **O que é:** gerador de código pra conversão entre objetos (Entity ↔ DTO).
- **Pra que serve aqui:** converter `PurchaseRequest` → `PurchaseRequestDTO`, `ApprovalStep` → `ApprovalStepDTO`, sem escrever isso na mão.
- **Pacote:** `org.mapstruct:mapstruct` (+ `mapstruct-processor` no annotation processing)
- **Nota:** não vem no Spring Initializr, precisa adicionar manualmente no `pom.xml`.

### Spring Boot Actuator
- **O que é:** endpoints prontos de monitoramento e saúde da aplicação.
- **Pra que serve aqui:** ter um `/actuator/health` — bom hábito profissional, útil pra debug.
- **Pacote:** `org.springframework.boot:spring-boot-starter-actuator`

---

## 4. Testes

### Spring Boot Starter Test
- **O que é:** já vem por padrão em qualquer projeto Spring Boot.
- **Pra que serve aqui:** testar a lógica de negócio, principalmente a `ApprovalService` (regras condicionais tipo "valor > 5000 → vai pro diretor").
- **Pacote:** `org.springframework.boot:spring-boot-starter-test`
- **Inclui:** JUnit 5, Mockito, AssertJ

### H2 Database
- **O que é:** banco de dados em memória.
- **Pra que serve aqui:** rodar os testes sem precisar do PostgreSQL/Docker ligado.
- **Pacote:** `com.h2database:h2` (escopo `test`)

---

## 5. Resumo — o que marcar agora no Initializr

```
[x] Spring Web
[x] Spring Data JPA
[x] PostgreSQL Driver
[x] Validation
[x] Lombok
[x] H2 Database        (escopo: Test)
[x] Spring Boot DevTools
```

**Deixar pra depois:**
- Spring Security + JWT (entra quando o fluxo de aprovação já estiver funcional)
- MapStruct (entra quando começar a ter muitos DTOs repetidos)
- Actuator (opcional, bom pra portfólio)

---

## 6. Ordem sugerida de uso no projeto

1. `Spring Web` + `Spring Data JPA` + `PostgreSQL Driver` → validar que a aplicação sobe e conecta no banco
2. `Lombok` + `Validation` → criar as entidades `User`, `PurchaseRequest`, `ApprovalStep`
3. `H2 Database` (test) → escrever os primeiros testes da `ApprovalService`
4. `Spring Boot DevTools` → acelerar o ciclo de desenvolvimento
5. `Spring Security` + `JWT` → só depois que o fluxo de aprovação estiver rodando com usuário fake
6. `MapStruct` → quando o número de DTOs começar a incomodar
7. `Actuator` → refinamento final, antes de colocar no portfólio