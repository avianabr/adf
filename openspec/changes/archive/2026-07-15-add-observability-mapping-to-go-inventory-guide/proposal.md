# Proposta: mapear observabilidade no roteiro de inventário Go

## Por quê

O roteiro cita observabilidade na análise arquitetural, mas não oferece uma
etapa estruturada para investigar como o codebase Go gera logs, métricas,
traces e demais telemetria. Sem esse mapeamento, fica difícil verificar sinais
operacionais, instrumentação de fluxos críticos, correlação e riscos de
exposição de dados.

## O que muda

- Acrescentar uma seção específica de observabilidade ao roteiro.
- Orientar o mapeamento de bibliotecas, configuração, inicialização e ciclo de
  vida de logs, métricas, tracing e exportadores de telemetria.
- Inventariar eventos e atributos observáveis por componente ou fluxo, incluindo
  níveis e estrutura de logs, métricas, spans, correlação, amostragem e destinos
  quando comprováveis.
- Exigir evidência para cobertura, tratamento de falhas de exportação e proteção
  de dados sensíveis, classificando comportamentos não comprovados como lacunas.

## Impacto

- Capacidade existente modificada: `go-application-inventory-guide`.
- Alteração exclusivamente documental; não há mudança em runtime, APIs ou
  dependências de aplicações analisadas.
