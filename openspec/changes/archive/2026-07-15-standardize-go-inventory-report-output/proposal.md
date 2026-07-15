# Proposta: padronizar o relatório de saída do inventário Go

## Por quê

O roteiro define a ordem do relatório e traz tabelas locais para algumas
investigações, mas não oferece um formato final consistente para todos os itens.
Isso deixa margem para relatórios com níveis de detalhe, evidências e tratamento
de lacunas diferentes, dificultando a comparação e a revisão dos resultados.

## O que muda

- Definir um template de relatório final em Markdown, com seções, títulos e
  ordem obrigatórios.
- Orientar o conteúdo e o formato esperado de cada seção, combinando resumos,
  tabelas, listas e blocos de evidência conforme o tipo de achado.
- Padronizar a representação de fatos, inferências, lacunas, perguntas abertas,
  confiança e referências ao codebase.
- Incluir instruções para não produzir seções vazias: ausências devem ser
  declaradas com escopo e evidência de busca, sem inferir ausência em
  infraestrutura externa.

## Impacto

- Capacidade existente modificada: `go-application-inventory-guide`.
- Alteração exclusivamente documental; não há mudança em runtime, APIs ou
  dependências de aplicações analisadas.
