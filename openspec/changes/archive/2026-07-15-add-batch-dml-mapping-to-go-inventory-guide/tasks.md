## 1. Roteiro de DML em lote

- [x] 1.1 Ampliar a seção de SQL/DML com a investigação específica de `INSERT`,
  `MERGE` e operações equivalentes em lote.
- [x] 1.2 Incluir a identificação de geração do lote, origem dos dados, tamanho
  ou critério de divisão e comandos executados.
- [x] 1.3 Incluir o mapeamento de transações, fronteiras e estratégia de commit
  por lote ou ao final do processamento.
- [x] 1.4 Incluir evidências sobre exceções, rollback, retry, resultados parciais
  e aspectos não comprovados.

## 2. Validação

- [x] 2.1 Verificar que o roteiro não infere tamanho de lote ou atomicidade sem
  evidência no codebase ou na configuração disponível.
- [x] 2.2 Verificar que cada lote inventariado exige referência ao código que o
  cria, executa e controla transacionalmente.
