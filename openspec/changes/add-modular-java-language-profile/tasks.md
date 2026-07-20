## 1. Estrutura modular do roteiro

- [x] 1.1 Extrair as regras de evidência, análise arquitetural, integrações,
  observabilidade, empacotamento e relatório para um núcleo independente de
  linguagem.
- [x] 1.2 Organizar o conteúdo específico de Go como perfil selecionável,
  preservando sua cobertura de módulos, pacotes, frameworks e pontos de entrada.
- [x] 1.3 Definir como selecionar e combinar núcleo e perfis, incluindo o
  tratamento de repositórios com mais de uma linguagem.

## 2. Perfil Java

- [x] 2.1 Criar um perfil Java que investigue versão/JDK, Maven, Gradle, fontes,
  recursos, módulos e artefatos de build.
- [x] 2.2 Incluir descoberta de pontos de entrada, frameworks e componentes Java,
  como `main`, Spring Boot, Jakarta, servlets, jobs e bibliotecas de teste.
- [x] 2.3 Incluir o inventário de dependências, plugins, configuração e testes a
  partir de `pom.xml`, `build.gradle`, `settings.gradle` e artefatos relacionados.

## 3. Documentação e validação

- [x] 3.1 Atualizar o README com instruções e prompts para seleção de perfil Go
  ou Java.
- [x] 3.2 Verificar que o núcleo não pressupõe uma linguagem e que o perfil Java
  não infere uso de framework apenas pela dependência declarada.
- [x] 3.3 Verificar que o formato final Markdown permanece único e verificável
  para todos os perfis.
