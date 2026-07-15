# Proposta: mapear sequências e auto-incremento no roteiro de inventário Go

## Por quê

O roteiro de GaussDB/PostgreSQL já cobre drivers, conexões, consultas e
migrações, mas não orienta a identificação explícita de sequências nem de
colunas cujo valor é gerado automaticamente. Essa lacuna reduz a
rastreabilidade da geração de identificadores, de seus limites e de possíveis
dependências entre schema, migrations e código Go.

## O que muda

- Ampliar o roteiro de GaussDB/PostgreSQL para localizar sequências e colunas
  com geração automática de valores, incluindo `SERIAL`, `BIGSERIAL`,
  `IDENTITY`, `DEFAULT nextval(...)` e mecanismos equivalentes comprovados.
- Orientar o relatório a relacionar sequência, coluna/tabela, tipo, parâmetros
  observáveis e local de definição ou alteração em DDL/migrations.
- Registrar como a aplicação obtém valores gerados — por exemplo, cláusulas
  `RETURNING`, leitura prévia de sequência ou comportamento de ORM — e apontar
  lacunas quando a relação não puder ser comprovada.

## Impacto

- Capacidade existente modificada: `go-application-inventory-guide`.
- Alteração exclusivamente documental; não há mudança em runtime, APIs ou
  dependências de aplicações analisadas.
