## ADDED Requirements

### Requirement: Roteiro guiado de inventário

O sistema SHALL disponibilizar um roteiro em Markdown que oriente um LLM a
inventariar uma aplicação escrita em Go a partir de seu codebase.

#### Scenario: Análise de um repositório Go desconhecido

- **WHEN** um LLM recebe um codebase Go e o roteiro
- **THEN** ele SHALL seguir etapas ordenadas de descoberta, análise arquitetural,
  análise funcional, consolidação e validação
- **AND** SHALL distinguir fatos observados de inferências.

### Requirement: Perspectiva arquitetural

O roteiro SHALL orientar a identificação de estrutura do repositório, módulos,
  pontos de entrada, componentes, dependências, fronteiras, persistência,
  integrações, configuração, observabilidade, segurança, entrega e riscos
  técnicos.

#### Scenario: Componentes e dependências identificados

- **WHEN** o LLM analisa a arquitetura
- **THEN** o relatório SHALL relacionar cada componente às suas responsabilidades,
  interfaces e dependências relevantes
- **AND** SHALL citar os arquivos, pacotes ou símbolos que sustentam cada achado.

### Requirement: Inventário de módulos, pacotes e frameworks

O roteiro SHALL orientar o LLM a examinar `go.mod`, `go.sum`, os `import`s e a
estrutura de pacotes para mapear módulos diretos, dependências relevantes,
pacotes internos e frameworks utilizados pela aplicação.

#### Scenario: Dependências técnicas identificadas

- **WHEN** o LLM examina uma aplicação Go
- **THEN** o relatório SHALL listar o módulo principal, pacotes próprios e
  dependências externas relevantes, com versão quando disponível
- **AND** SHALL associar cada dependência ao seu propósito e aos pontos em que é
  utilizada
- **AND** SHALL destacar separadamente frameworks, drivers de banco de dados e
  bibliotecas de cliente Kafka.

### Requirement: Mapeamento de Kafka

O roteiro SHALL orientar o LLM a identificar e documentar o uso de Kafka pela
aplicação, incluindo as bibliotecas de cliente, produtores, consumidores,
tópicos, grupos de consumidores, formatos de mensagem, configuração e garantias
de entrega observáveis no código.

#### Scenario: Aplicação usa Kafka

- **WHEN** importações, configurações ou código indicarem integração com Kafka
- **THEN** o relatório SHALL identificar a biblioteca utilizada e sua versão
  quando disponível
- **AND** SHALL mapear, para cada produtor ou consumidor, o pacote responsável,
  tópico, grupo, contrato de mensagem, serialização e fluxos funcionais atendidos
- **AND** SHALL registrar evidências sobre retries, commits, idempotência, DLQ,
  ordenação, segurança e tratamento de falhas, classificando os itens ausentes
  como lacunas.

### Requirement: Mapeamento de GaussDB e PostgreSQL

O roteiro SHALL orientar o LLM a identificar e documentar o acesso da aplicação a
GaussDB ou PostgreSQL, incluindo driver, biblioteca de acesso, configuração de
conexão, repositórios, esquemas, consultas, transações e migrações.

#### Scenario: Aplicação acessa GaussDB ou PostgreSQL

- **WHEN** importações, DSNs, configuração ou código indicarem acesso a GaussDB
  ou PostgreSQL
- **THEN** o relatório SHALL identificar o driver e as bibliotecas de abstração ou
  ORM utilizadas, com versão quando disponível
- **AND** SHALL mapear os pacotes responsáveis, pool de conexões, modelos ou
  tabelas, operações de leitura/escrita, transações e mecanismos de migração
- **AND** SHALL indicar compatibilidades assumidas entre GaussDB e PostgreSQL,
  configuração de segurança e falhas ou riscos observáveis.

### Requirement: Inventário de consultas SQL e operações DML

O roteiro SHALL orientar o LLM a localizar SQL literal, queries construídas em
tempo de execução, arquivos de query e chamadas de bibliotecas de acesso a dados.
O relatório SHALL inventariar `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE` e
outras operações DML executadas ou geradas pela aplicação.

#### Scenario: Comando SQL identificado

- **WHEN** uma consulta ou operação DML for encontrada
- **THEN** o relatório SHALL registrar seu identificador, localização no código,
  pacote responsável, operação, tabelas ou visões afetadas, parâmetros e fluxo
  funcional associado
- **AND** SHALL preservar ou resumir o comando de forma que sua intenção e
  predicados relevantes sejam verificáveis
- **AND** SHALL sinalizar SQL dinâmico e identificar quais partes não puderam ser
  determinadas estaticamente.

### Requirement: Índice de complexidade SQL

O roteiro SHALL atribuir a cada consulta ou operação DML um índice de
complexidade de 1 a 5, acompanhado dos critérios que justificam a classificação.

#### Scenario: Consulta classificada

- **WHEN** uma consulta ou operação DML for inventariada
- **THEN** o relatório SHALL classificá-la como:
  - **1 — simples:** uma tabela, operação direta, sem subconsulta, agregação ou
    junção;
  - **2 — moderada:** filtros, ordenação, paginação ou agregação simples;
  - **3 — composta:** múltiplas tabelas, junções, CTE ou subconsulta;
  - **4 — avançada:** múltiplas CTEs/subconsultas, janelas, `MERGE`, lote ou
    lógica condicional relevante;
  - **5 — crítica:** SQL dinâmico complexo, múltiplas etapas dependentes,
    procedimentos/funções, alto volume potencial ou semântica transacional
    difícil de verificar
- **AND** SHALL registrar os fatores observados que determinaram o índice.

### Requirement: Mapeamento de tipos CLOB, BLOB e JSON

O roteiro SHALL orientar o LLM a mapear o uso de CLOB, BLOB e JSON em GaussDB ou
PostgreSQL e suas representações no código Go.

#### Scenario: Tipo especial identificado

- **WHEN** esquema, migração, query, struct Go ou biblioteca de serialização
  indicar uso de CLOB, BLOB ou JSON/JSONB
- **THEN** o relatório SHALL registrar coluna ou atributo, tipo no banco,
  representação Go, pacote responsável e operações que leem ou escrevem o valor
- **AND** SHALL indicar conversões, serialização, streaming, tamanho potencial e
  cuidados observáveis de integridade, desempenho ou segurança
- **AND** SHALL associar o tipo aos fluxos funcionais e interfaces que o expõem
  ou processam, quando essa relação puder ser comprovada.

### Requirement: Perspectiva funcional

O roteiro SHALL orientar a identificação de capacidades de negócio, atores,
  canais de entrada, fluxos principais, regras de negócio, efeitos colaterais e
  estados tratados pela aplicação.

#### Scenario: Fluxo funcional documentado

- **WHEN** uma capacidade for inferida de handlers, comandos, casos de uso ou
  testes
- **THEN** o relatório SHALL descrever gatilho, pré-condições, etapas,
  dados afetados, resultado e falhas conhecidas
- **AND** SHALL registrar o grau de confiança quando o domínio não estiver
  explícito no codebase.

### Requirement: Relatório verificável

O roteiro SHALL definir um formato de saída que separe inventário, evidências,
  lacunas, hipóteses e perguntas em aberto.

#### Scenario: Evidência insuficiente

- **WHEN** uma conclusão não puder ser comprovada pelo codebase
- **THEN** o LLM SHALL classificá-la como hipótese ou lacuna
- **AND** SHALL indicar a evidência adicional necessária para confirmá-la.
