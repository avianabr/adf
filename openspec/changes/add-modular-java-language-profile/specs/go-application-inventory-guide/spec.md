## ADDED Requirements

### Requirement: Perfis extensíveis de linguagem

O sistema SHALL disponibilizar um núcleo de roteiro independente de linguagem e
perfis de linguagem selecionáveis, de modo que a análise compartilhe regras de
evidência e relatório sem aplicar convenções específicas fora de seu perfil.

#### Scenario: Perfil de linguagem selecionado

- **WHEN** o LLM recebe um codebase e uma linguagem ou perfil selecionado
- **THEN** SHALL combinar o núcleo comum com o perfil correspondente
- **AND** SHALL usar apenas artefatos, convenções e critérios de descoberta
  comprováveis para o perfil selecionado
- **AND** SHALL manter o formato final de relatório Markdown e as regras de
  evidência, confiança, hipóteses e lacunas do núcleo comum.

#### Scenario: Repositório com mais de uma linguagem

- **WHEN** o codebase contiver artefatos de mais de um perfil disponível
- **THEN** o LLM SHALL identificar os perfis aplicáveis e registrar o escopo de
  cada um
- **AND** SHALL evitar atribuir um artefato ao perfil incorreto
- **AND** SHALL classificar como lacuna qualquer relação entre componentes de
  linguagens diferentes que não possa ser comprovada.

### Requirement: Perfil Java

O sistema SHALL disponibilizar um perfil Java que oriente o LLM a inventariar uma
aplicação Java a partir de seus artefatos de build, código, recursos, configuração
e testes disponíveis.

#### Scenario: Aplicação Java analisada

- **WHEN** o LLM analisa um codebase Java com o perfil Java selecionado
- **THEN** SHALL identificar versão ou toolchain Java quando disponível,
  Maven/Gradle e seus módulos, dependências, plugins, fontes, recursos, testes e
  artefatos de build
- **AND** SHALL localizar pontos de entrada, componentes e frameworks por uso
  concreto, como `main`, Spring Boot, Jakarta, servlets, jobs ou bibliotecas
  equivalentes
- **AND** SHALL citar os arquivos, pacotes, classes, métodos, configurações ou
  testes que sustentam cada achado
- **AND** SHALL classificar como hipótese ou lacuna qualquer framework,
  comportamento de execução ou configuração que não possa ser comprovado pelo
  codebase ou configuração disponível.
