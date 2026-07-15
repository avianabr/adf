# Proposta: mapear DML em lote no roteiro de inventário Go

## Por quê

O roteiro inventaria operações DML e já classifica lotes como SQL avançado, mas
não determina como identificar a formação, o tamanho e o controle transacional
dos lotes. Isso pode ocultar riscos de desempenho, atomicidade, commit parcial e
recuperação de erro em operações de `INSERT` ou `MERGE` executadas pela aplicação
Go.

## O que muda

- Ampliar o roteiro de SQL/DML para identificar operações em lote, com foco em
  `INSERT`, `MERGE` e mecanismos equivalentes de driver, ORM ou query builder.
- Orientar o relatório a registrar como os lotes são gerados, sua quantidade de
  registros ou critério configurável de divisão, dados e comandos produzidos.
- Mapear transações, limites de commit, commit por lote ou final, erros,
  rollback, retry e possibilidades de resultado parcial somente quando
  comprováveis.

## Impacto

- Capacidade existente modificada: `go-application-inventory-guide`.
- Alteração exclusivamente documental; não há mudança em runtime, APIs ou
  dependências de aplicações analisadas.
