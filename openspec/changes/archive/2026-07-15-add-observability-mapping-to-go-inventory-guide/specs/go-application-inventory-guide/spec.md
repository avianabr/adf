## ADDED Requirements

### Requirement: Mapeamento de observabilidade

O roteiro SHALL orientar o LLM a identificar e documentar como a aplicação Go
gera e exporta logs, métricas, traces e outras telemetrias observáveis no
codebase ou em sua configuração disponível.

#### Scenario: Aplicação possui instrumentação de observabilidade

- **WHEN** imports, configuração ou código indicarem geração ou exportação de
  logs, métricas, traces ou telemetria
- **THEN** o relatório SHALL identificar as bibliotecas utilizadas e suas versões
  quando disponíveis, bem como os pacotes responsáveis por inicialização,
  configuração, propagação de contexto e encerramento
- **AND** SHALL registrar, por componente ou fluxo, eventos e níveis de log,
  métricas, spans, atributos, correlação, amostragem e destinos ou exportadores
  quando observáveis
- **AND** SHALL relacionar cada sinal ao fluxo funcional ou operacional que ele
  representa, com arquivo, pacote ou símbolo que sustente o achado.

#### Scenario: Cobertura e segurança de observabilidade analisadas

- **WHEN** o LLM analisa a observabilidade de uma aplicação
- **THEN** o relatório SHALL registrar evidências sobre cobertura de fluxos
  críticos, falhas de instrumentação ou exportação, retries, buffering, perda ou
  degradação de telemetria quando observáveis
- **AND** SHALL registrar evidências sobre mascaramento, filtragem ou exposição
  de dados sensíveis em logs e atributos de telemetria
- **AND** SHALL classificar como lacuna qualquer garantia de cobertura,
  confiabilidade, retenção, amostragem ou proteção de dados que não possa ser
  comprovada pelo codebase ou pela configuração disponível.
