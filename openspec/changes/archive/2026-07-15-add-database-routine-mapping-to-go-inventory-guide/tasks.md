## 1. Roteiro de procedures e functions

- [x] 1.1 Ampliar a seção GaussDB/PostgreSQL com a investigação de procedures e
  functions definidas e utilizadas pela aplicação.
- [x] 1.2 Incluir assinatura, linguagem, parâmetros, retorno, objetos afetados e
  localização da definição ou alteração em DDL/migrations.
- [x] 1.3 Incluir o rastreamento de chamadas por SQL, driver ou ORM até o pacote,
  símbolo e fluxo funcional Go responsável.
- [x] 1.4 Incluir evidências sobre transações, erros, permissões e efeitos
  colaterais, classificando como lacuna os aspectos não comprovados.

## 2. Validação

- [x] 2.1 Verificar que o roteiro distingue function de procedure e definição de
  rotina de chamada efetivamente observada.
- [x] 2.2 Verificar que cada vínculo entre rotina e codebase Go exige referência
  ao arquivo, pacote, símbolo, query ou migration correspondente.
