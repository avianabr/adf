## 1. Roteiro de sequências e auto-incremento

- [x] 1.1 Ampliar a seção GaussDB/PostgreSQL com a investigação de sequências e
  colunas com valores gerados automaticamente.
- [x] 1.2 Incluir os mecanismos observáveis, a relação sequência-coluna-tabela
  e os parâmetros relevantes de geração.
- [x] 1.3 Incluir o rastreamento de como o código Go, SQL ou ORM recebe ou usa
  os valores gerados.
- [x] 1.4 Exigir evidência para cada achado e classificação de hipóteses ou
  lacunas não comprovadas.

## 2. Validação

- [x] 2.1 Verificar que o roteiro distingue sequências explícitas de mecanismos
  de geração automática implícitos.
- [x] 2.2 Verificar que cada relação entre sequence, coluna, tabela e fluxo tem
  referência ao codebase analisado.
