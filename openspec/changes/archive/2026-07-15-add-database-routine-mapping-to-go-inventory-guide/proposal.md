# Proposta: mapear procedures e functions no roteiro de inventário Go

## Por quê

O roteiro já orienta a localizar funções e procedimentos em migrations e DDL,
mas não define como relacioná-los às chamadas da aplicação Go. Sem esse
detalhamento, regras e operações executadas no banco podem ficar fora do
inventário funcional, sem rastreabilidade de parâmetros, resultados,
efeitos colaterais e transações.

## O que muda

- Ampliar o roteiro de GaussDB/PostgreSQL para mapear procedures e functions
  definidos no schema e chamados, direta ou indiretamente, pela aplicação Go.
- Registrar assinatura, linguagem, localização da definição, parâmetros,
  retorno, objetos afetados e efeitos observáveis da rotina.
- Relacionar chamadas SQL, abstrações de driver/ORM e fluxos funcionais às
  rotinas, preservando evidências de transação, erros, permissões e pontos que
  não possam ser determinados estaticamente.

## Impacto

- Capacidade existente modificada: `go-application-inventory-guide`.
- Alteração exclusivamente documental; não há mudança em runtime, APIs ou
  dependências de aplicações analisadas.
