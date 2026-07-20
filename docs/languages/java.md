# Perfil de linguagem: Java

Use este perfil com o [núcleo do roteiro](../application-inventory-guide.md)
quando o repositório contiver fontes Java, `pom.xml`, `build.gradle`,
`build.gradle.kts` ou `settings.gradle`. Não conclua que uma dependência ou
anotação isolada habilita um framework sem evidência de uso ou configuração.

## Descoberta, módulos e build

1. Localize `pom.xml`, `.mvn/`, `mvnw`, `build.gradle`, `build.gradle.kts`,
   `settings.gradle`, `settings.gradle.kts`, `gradlew` e arquivos de catálogo de
   versões. Registre Maven ou Gradle, módulos, plugins, repositórios e tasks
   somente quando observáveis.
2. Identifique versão ou toolchain Java em `maven-compiler-plugin`, propriedades,
   `toolchain`, `sourceCompatibility`, `targetCompatibility`, pipelines ou
   imagens de build. Classifique versões conflitantes como lacuna ou risco.
3. Mapeie `src/main/java`, `src/main/resources`, `src/test/java`,
   `src/test/resources`, módulos multi-projeto, JAR/WAR e artefatos de build.
4. Relacione comandos Maven/Gradle, scripts e pipelines ao módulo e ao artefato
   produzido — por exemplo, JAR executável, biblioteca ou WAR — quando comprovado.

## Pontos de entrada, frameworks e componentes

1. Localize `public static void main(String[] args)`, classes configuradas como
   entrada e comandos/serviços iniciados pelo build ou container.
2. Identifique Spring Boot, Spring MVC, Spring Data, Jakarta EE, JAX-RS,
   servlets, beans CDI/EJB, schedulers, consumers e jobs por anotações, classes,
   configuração e inicialização concretas. A presença de uma dependência não é
   evidência suficiente.
3. Para cada componente, registre pacote, classe, método, anotação, recurso de
   configuração e fluxo atendido. Trace controllers, endpoints, handlers,
   serviços, repositórios, listeners e encerramento quando observáveis.
4. Procure bibliotecas de acesso e integração por chamadas concretas, como JDBC,
   JPA/Hibernate, Spring Data, clientes Kafka e clientes Redis; use o núcleo para
   inventariar o comportamento específico de banco, mensageria ou cache.

## Dependências, configuração e testes

1. Inventarie dependências e plugins de `dependencies`, `dependencyManagement`,
   `plugins`, profiles Maven/Gradle e catálogos de versão. Registre escopo e
   versão quando disponíveis.
2. Localize `application.properties`, `application.yml`, perfis Spring, recursos
   em `src/main/resources`, variáveis de ambiente e arquivos externos sem expor
   valores secretos.
3. Mapeie JUnit, TestNG, Mockito, Spring Test, testes de integração e fixtures a
   partir de fontes de teste, plugins e execução observada.
4. Cite arquivo, pacote, classe, método, anotação, `pom.xml` ou arquivo Gradle em
   cada achado específico do perfil.

| Item Java | Localização | Papel observado | Confiança |
|---|---|---|---|
| Build/módulo | `pom.xml` ou `build.gradle[.kts]` | Maven/Gradle, versão e módulos | Alta |
| Fonte/recurso | `src/main/...` | Componente ou configuração | Média/Alta |
| Entrada | classe com `main` ou configuração de framework | Inicialização observada | Alta |
| Teste | `src/test/...` | Cobertura e ferramentas de teste | Média/Alta |

