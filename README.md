# Roteiro de inventário para aplicações

Este projeto fornece um roteiro em Markdown para orientar um LLM na análise
arquitetural e funcional de codebases. O resultado é um inventário
verificável: cada conclusão deve apontar para código, configuração, migration ou
teste que a sustente.

O roteiro é modular:

- [Núcleo comum](docs/application-inventory-guide.md): regras de evidência,
  arquitetura, integrações, observabilidade, empacotamento e relatório final.
- [Perfil Go](docs/languages/go.md): `go.mod`, pacotes, binários e ferramentas Go.
- [Perfil Java](docs/languages/java.md): JDK, Maven/Gradle, fontes, recursos e
  frameworks Java.

## Como executar o roteiro

1. Identifique os perfis aplicáveis pelos artefatos do repositório: use Go para
   `go.mod`/`go.work` e Java para `pom.xml` ou `build.gradle`/`build.gradle.kts`.
2. Forneça ao LLM o núcleo e todos os perfis aplicáveis, além do codebase,
   configurações, migrations, manifests de entrega e testes disponíveis.
3. Em um repositório multilíngue, aplique cada perfil somente ao seu escopo e
   registre os limites e as relações comprovadas entre componentes.
4. Use um prompt como os exemplos abaixo, substituindo o caminho e qualquer
   restrição de escopo.
5. Revise o relatório gerado. Achados devem conter referências ao repositório;
   hipóteses, lacunas e perguntas abertas não devem ser apresentados como fatos.

O roteiro cobre, entre outros temas: arquitetura, dependências, fluxos
funcionais, Kafka, GaussDB/PostgreSQL, SQL e DML em lote, Redis, dados
CLOB/BLOB/JSON, observabilidade, empacotamento e execução em containers ou
Kubernetes, além do formato padronizado do relatório.

## Empacotamento e execução

Para mapear como a aplicação é preparada para rodar, disponibilize também os
artefatos de entrega que existirem: Dockerfiles, arquivos Compose, Makefiles,
scripts de build, pipelines de CI/CD, manifests Kubernetes, charts Helm e overlays
Kustomize. O roteiro identifica o que é comprovado nesses arquivos — build,
imagem, comando, portas, configuração, recursos, probes e permissões — sem
presumir que um artefato esteja aplicado em um ambiente real.

## Prompt para Go

```text
Analise o codebase Go localizado em <CAMINHO_DO_CODEBASE> usando:
- <CAMINHO_DESTE_PROJETO>/docs/application-inventory-guide.md
- <CAMINHO_DESTE_PROJETO>/docs/languages/go.md

Escopo: analise código Go, go.mod/go.sum, configurações, migrations, arquivos
SQL, testes, Dockerfiles, Compose, Makefiles, pipelines, manifests Kubernetes,
charts Helm e overlays Kustomize disponíveis no repositório. Para os artefatos de
entrega, mapeie build, imagens, execução, rede, configuração, recursos, probes e
permissões somente quando forem comprovados. Não acesse nem suponha informações
de infraestrutura que não estejam nesses artefatos.

Produza o relatório final estritamente no template Markdown definido na seção
"Consolidação e validação" do roteiro. Para cada achado, cite caminho relativo e
linha ou símbolo quando disponível, atribua confiança alta, média ou baixa e
separe claramente fatos, inferências, lacunas e perguntas em aberto.

Não exponha valores secretos. Se não houver evidência suficiente, registre uma
lacuna, os locais examinados e a evidência necessária para confirmar a conclusão.
```

## Prompt para Java

```text
Analise o codebase Java localizado em <CAMINHO_DO_CODEBASE> usando:
- <CAMINHO_DESTE_PROJETO>/docs/application-inventory-guide.md
- <CAMINHO_DESTE_PROJETO>/docs/languages/java.md

Escopo: analise pom.xml, build.gradle/build.gradle.kts, settings.gradle, fontes e
recursos em src/main, testes em src/test, configurações, migrations, arquivos SQL,
Dockerfiles, pipelines e manifests de entrega disponíveis. Identifique Maven ou
Gradle, versão/JDK, módulos, dependências, plugins, pontos de entrada e
frameworks somente por uso concreto ou configuração comprovada.

Produza o relatório final no template Markdown do núcleo. Para cada achado, cite
o caminho relativo e classe, método, anotação ou linha quando disponível, com
confiança alta, média ou baixa. Separe fatos, inferências, lacunas e perguntas em
aberto e não exponha valores secretos.
```

## Saída esperada

O relatório inclui resumo e escopo, arquitetura, dependências, fluxos, integrações
técnicas, observabilidade, empacotamento/execução e riscos. Seu formato é único
para todos os perfis. Se uma área não apresentar achados, o LLM deve declarar o
escopo e as evidências de busca, sem concluir que um comportamento não existe fora
do repositório.
