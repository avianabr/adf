## MODIFIED Requirements

### Requirement: Relatório verificável

O roteiro SHALL definir um formato de saída em Markdown que separe inventário,
evidências, lacunas, hipóteses e perguntas em aberto e oriente o conteúdo
esperado para cada seção do relatório.

#### Scenario: Relatório de inventário produzido

- **WHEN** o LLM conclui a análise de um codebase Go
- **THEN** SHALL produzir um relatório em Markdown com seções ordenadas para
  resumo e escopo, arquitetura, dependências, fluxos funcionais, Kafka,
  GaussDB/PostgreSQL, SQL/DML, Redis, tipos especiais, observabilidade e riscos
- **AND** SHALL usar títulos, tabelas, listas e blocos de evidência conforme o
  template do roteiro para tornar os achados comparáveis e verificáveis
- **AND** SHALL registrar para cada item relevante sua conclusão, confiança e
  referências a arquivos, pacotes, símbolos, configurações ou testes que a
  sustentem
- **AND** SHALL apresentar fatos, inferências, lacunas e perguntas em aberto em
  formatos explicitamente identificados
- **AND** SHALL declarar seções sem achados com o escopo e a evidência de busca,
  sem concluir ausência de comportamento em infraestrutura externa.

#### Scenario: Evidência insuficiente

- **WHEN** uma conclusão não puder ser comprovada pelo codebase
- **THEN** o LLM SHALL classificá-la como hipótese ou lacuna
- **AND** SHALL indicar a evidência adicional necessária para confirmá-la.
