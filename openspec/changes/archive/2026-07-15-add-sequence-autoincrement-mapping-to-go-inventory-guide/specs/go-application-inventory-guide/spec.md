## MODIFIED Requirements

### Requirement: Mapeamento de GaussDB e PostgreSQL

O roteiro SHALL orientar o LLM a identificar e documentar o acesso da aplicação
a GaussDB ou PostgreSQL, incluindo driver, biblioteca de acesso, configuração de
conexão, repositórios, esquemas, consultas, transações, migrações, sequências e
colunas com valores gerados automaticamente.

#### Scenario: Aplicação acessa GaussDB ou PostgreSQL

- **WHEN** importações, DSNs, configuração ou código indicarem acesso a GaussDB
  ou PostgreSQL
- **THEN** o relatório SHALL identificar o driver e as bibliotecas de abstração ou
  ORM utilizadas, com versão quando disponível
- **AND** SHALL mapear os pacotes responsáveis, pool de conexões, modelos ou
  tabelas, operações de leitura/escrita, transações e mecanismos de migração
- **AND** SHALL indicar compatibilidades assumidas entre GaussDB e PostgreSQL,
  configuração de segurança e falhas ou riscos observáveis.

#### Scenario: Sequência ou geração automática de valor identificada

- **WHEN** DDL, migration, query, ORM ou configuração indicar uma sequência ou
  geração automática de valor em GaussDB ou PostgreSQL
- **THEN** o relatório SHALL registrar a sequência ou o mecanismo observado,
  como `SERIAL`, `BIGSERIAL`, `IDENTITY` ou `DEFAULT nextval(...)`, sem inferir
  mecanismos ausentes
- **AND** SHALL relacioná-lo à tabela e coluna afetadas, ao tipo e aos parâmetros
  observáveis, como valor inicial, incremento, mínimo, máximo e ciclo, com a
  localização da definição ou alteração
- **AND** SHALL identificar como a aplicação obtém, recebe ou utiliza o valor
  gerado, incluindo `RETURNING`, leitura explícita da sequência ou comportamento
  de ORM quando comprovável
- **AND** SHALL classificar como hipótese ou lacuna qualquer relação, garantia de
  unicidade, tratamento de overflow ou comportamento de geração que não possa
  ser comprovado pelo codebase ou configuração disponível.
