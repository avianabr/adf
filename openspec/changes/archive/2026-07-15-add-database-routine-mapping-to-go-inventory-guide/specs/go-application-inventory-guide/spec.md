## MODIFIED Requirements

### Requirement: Mapeamento de GaussDB e PostgreSQL

O roteiro SHALL orientar o LLM a identificar e documentar o acesso da aplicação
a GaussDB ou PostgreSQL, incluindo driver, biblioteca de acesso, configuração de
conexão, repositórios, esquemas, consultas, transações, migrações, sequências,
colunas com valores gerados automaticamente, functions e procedures.

#### Scenario: Aplicação acessa GaussDB ou PostgreSQL

- **WHEN** importações, DSNs, configuração ou código indicarem acesso a GaussDB
  ou PostgreSQL
- **THEN** o relatório SHALL identificar o driver e as bibliotecas de abstração ou
  ORM utilizadas, com versão quando disponível
- **AND** SHALL mapear os pacotes responsáveis, pool de conexões, modelos ou
  tabelas, operações de leitura/escrita, transações e mecanismos de migração
- **AND** SHALL indicar compatibilidades assumidas entre GaussDB e PostgreSQL,
  configuração de segurança e falhas ou riscos observáveis.

#### Scenario: Function ou procedure identificada

- **WHEN** DDL, migration, query, ORM ou código Go indicar uma function ou
  procedure de GaussDB ou PostgreSQL
- **THEN** o relatório SHALL distinguir a function da procedure e registrar
  nome qualificado, assinatura, linguagem, parâmetros, retorno quando aplicável,
  objetos afetados e localização da definição ou alteração
- **AND** SHALL relacionar cada chamada observada — como `SELECT`, `CALL` ou
  abstração de driver/ORM — ao arquivo, pacote ou símbolo Go responsável e ao
  fluxo funcional associado, quando comprovável
- **AND** SHALL registrar evidências sobre transação, tratamento de erros,
  permissões e efeitos colaterais observáveis
- **AND** SHALL classificar como hipótese ou lacuna qualquer assinatura, efeito,
  garantia transacional, permissão ou chamada que não possa ser comprovada pelo
  codebase ou pela configuração disponível.
