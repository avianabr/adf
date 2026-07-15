# Proposta: mapear empacotamento e execução no roteiro de inventário Go

## Por quê

O roteiro cita artefatos de entrega na descoberta e na arquitetura, mas não
orienta uma análise estruturada de como a aplicação é construída, empacotada e
executada. Isso pode ocultar decisões relevantes de imagem, runtime, configuração
e operação em Docker ou Kubernetes.

## O que muda

- Acrescentar uma seção específica para mapear build, artefatos, imagens e
  configuração de execução da aplicação Go.
- Cobrir Dockerfiles, Compose, scripts, CI/CD e registros de imagem quando
  disponíveis, incluindo estágios de build, base, binário, entrypoint, usuário,
  portas, volumes e variáveis de ambiente.
- Cobrir manifests Kubernetes, Helm e Kustomize, identificando workloads, imagens,
  serviços, ingressos, configuração, segredos, probes, recursos, escalonamento,
  volumes e identidade/permissões quando comprovados.
- Exigir evidências para diferenças entre ambientes, segurança e riscos
  operacionais, distinguindo artefatos presentes de configurações efetivamente
  aplicadas.

## Impacto

- Capacidade existente modificada: `go-application-inventory-guide`.
- Alteração exclusivamente documental; não há mudança em runtime, APIs ou
  dependências de aplicações analisadas.
