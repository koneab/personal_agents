---
description: Spring Security configuration and secure-coding rules for Spring Boot services.
applyTo: 'src/main/java/**/*.java,src/main/resources/application*.yml,src/main/resources/application*.yaml,src/main/resources/application*.properties'
---

## Configuration
- Declare a `SecurityFilterChain` bean; do not extend the removed `WebSecurityConfigurerAdapter`.
- Deny by default: end the matcher list with `anyRequest().authenticated()` and permit only named public endpoints.
- Use `requestMatchers(...)` with explicit paths and HTTP methods.
- Enable method security (`@EnableMethodSecurity`) and protect service methods with `@PreAuthorize` where authorization depends on the resource or user.
- Authorize on the server for every request; never rely on hidden UI elements or client-side checks.

## Authentication and secrets
- Hash passwords with `DelegatingPasswordEncoder` / `BCryptPasswordEncoder` or Argon2; never store plaintext or use MD5/SHA-1.
- Prefer OAuth2 resource server with JWT validation for APIs; validate issuer, audience and expiry.
- Never hard-code secrets, keys, tokens or passwords in code, `application*.yml` or `application*.properties`; read them from environment variables or a secrets manager.
- Never log credentials, tokens or full request bodies containing personal data.

## Web protections
- Keep CSRF protection enabled for browser-session applications; disable it only for stateless token APIs and document the reason in a comment.
- Configure CORS with explicit origins, methods and headers; never `*` together with credentials.
- Keep Spring Security's default security headers; set a restrictive `Content-Security-Policy` for browser-facing apps.
- Require HTTPS in non-local environments.

## Input and output
- Validate all external input at the controller boundary with Bean Validation; reject unknown or oversized payloads.
- Use parameterised queries only; never build SQL, JPQL or shell commands from user input.
- Do not use Java native serialization or enable Jackson default typing for untrusted data.
- Check object ownership on every lookup by identifier to prevent insecure direct object references.
- Return generic error messages for authentication failures; do not reveal whether a user exists.

## Dependencies and actuator
- Do not add dependencies with known vulnerabilities; keep Spring Boot on a supported release line.
- Expose only `health` and `info` Actuator endpoints publicly; secure all others.
