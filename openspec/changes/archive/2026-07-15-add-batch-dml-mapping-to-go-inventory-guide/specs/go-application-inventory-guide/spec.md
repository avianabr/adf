## MODIFIED Requirements

### Requirement: Inventário de consultas SQL e operações DML

O roteiro SHALL orientar o LLM a localizar SQL literal, queries construídas em
tempo de execução, arquivos de query e chamadas de bibliotecas de acesso a dados.
O relatório SHALL inventariar `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE` e
outras operações DML executadas ou geradas pela aplicação, incluindo operações em
lote quando observáveis.

#### Scenario: Comando SQL identificado

- **WHEN** uma consulta ou operação DML for encontrada
- **THEN** o relatório SHALL registrar seu identificador, localização no código,
  pacote responsável, operação, tabelas ou visões afetadas, parâmetros e fluxo
  funcional associado
- **AND** SHALL preservar ou resumir o comando de forma que sua intenção e
  predicados relevantes sejam verificáveis
- **AND** SHALL sinalizar SQL dinâmico e identificar quais partes não puderam ser
  determinadas estaticamente.

#### Scenario: Operação DML em lote identificada

- **WHEN** SQL, driver, ORM, query builder ou código Go indicar uma operação DML
  em lote, especialmente `INSERT`, `MERGE` ou mecanismo equivalente
- **THEN** o relatório SHALL registrar como o lote é formado, sua origem de
  dados, o tamanho ou critério de divisão e os comandos ou chamadas executados,
  quando observáveis
- **AND** SHALL relacionar o lote ao arquivo, pacote ou símbolo Go responsável,
  às tabelas ou visões afetadas e ao fluxo funcional associado
- **AND** SHALL registrar a fronteira transacional e a estratégia de commit —
  por lote, ao final ou outra — quando comprovável
- **AND** SHALL registrar o tratamento de exceções, rollback, retry e a
  possibilidade de resultado parcial quando observáveis
- **AND** SHALL classificar como hipótese ou lacuna qualquer tamanho de lote,
  atomicidade, política de commit, recuperação ou comportamento de erro que não
  possa ser comprovado pelo codebase ou pela configuração disponível.
