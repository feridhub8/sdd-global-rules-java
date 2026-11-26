# Java

## Decided per project

Decide these with me for each project and record the decision in the project's `openspec/config.yaml`:

- Java version.
- Framework and its version (for example Spring Boot).
- Build tool and DSL. Whatever is chosen, always use its committed wrapper (`./gradlew`, `./mvnw`), never a globally installed one.
- Mapping library.
- Whether to use Lombok.
- Detailed architecture: package layout and any extra layers.

## Packages

- Base package: `com.<project>.<service>`, all lowercase, no separators (for example `com.xbank.account`).

## Layers

- The default flow is Controller → Service → Repository. No mediator, no CQRS libraries.

## Code style

- DTOs are regular classes, not Java records.
- Constructor injection into `private final` fields. No field injection (`@Autowired` on fields).
- File name equals the class name; one top-level class per file.
