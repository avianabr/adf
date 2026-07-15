## ADDED Requirements

### Requirement: Mapeamento de empacotamento e execução

O roteiro SHALL orientar o LLM a identificar e documentar como a aplicação Go é
construída, empacotada e configurada para execução, incluindo tecnologias de
container e orquestração quando observáveis no codebase ou em seus artefatos de
entrega.

#### Scenario: Artefato de container ou build identificado

- **WHEN** Dockerfile, Compose, script, Makefile, pipeline CI/CD ou configuração
  de registro de imagem indicar empacotamento da aplicação
- **THEN** o relatório SHALL registrar o artefato, seus estágios de build, imagem
  base, binário ou artefato produzido, entrypoint/comando, usuário, portas,
  volumes e configuração de runtime quando observáveis
- **AND** SHALL relacionar o artefato ao módulo ou binário Go responsável e aos
  ambientes ou pipelines que o utilizam, quando comprovável
- **AND** SHALL classificar como lacuna qualquer tag, imagem publicada, etapa de
  pipeline ou configuração de execução que não possa ser comprovada.

#### Scenario: Configuração Kubernetes identificada

- **WHEN** manifest Kubernetes, Helm, Kustomize ou configuração equivalente
  indicar a execução da aplicação em orquestrador
- **THEN** o relatório SHALL registrar workloads, imagens, réplicas, serviços,
  ingressos, ConfigMaps, referências a Secrets, probes, recursos, autoscaling,
  volumes e identidade ou permissões quando observáveis
- **AND** SHALL relacionar cada recurso ao artefato e à configuração de aplicação
  que ele referencia, sem expor valores secretos
- **AND** SHALL registrar evidências sobre diferenças entre ambientes, segurança
  de runtime e riscos operacionais
- **AND** SHALL classificar como hipótese ou lacuna qualquer recurso aplicado,
  permissão efetiva, valor secreto ou comportamento de cluster que não possa ser
  comprovado pelo codebase ou pela configuração disponível.
