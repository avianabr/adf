# Roteiro de inventário para aplicações Go

Este projeto fornece um roteiro em Markdown para orientar um LLM na análise
arquitetural e funcional de um codebase Go. O resultado é um inventário
verificável: cada conclusão deve apontar para código, configuração, migration ou
teste que a sustente.

O roteiro está em [docs/go-application-inventory-guide.md](docs/go-application-inventory-guide.md).

## Como executar o roteiro

1. Disponibilize ao LLM o codebase Go que será analisado, incluindo arquivos de
   configuração, `go.mod`, migrations, manifests de entrega e testes, quando
   existirem.
2. Forneça também o conteúdo do roteiro ou aponte o LLM para o arquivo em
   `docs/`.
3. Use um prompt como o exemplo abaixo, substituindo o caminho e qualquer
   restrição de escopo.
4. Revise o relatório gerado. Achados devem conter referências ao repositório;
   hipóteses, lacunas e perguntas abertas não devem ser apresentados como fatos.

O roteiro cobre, entre outros temas: arquitetura, dependências, fluxos
funcionais, Kafka, GaussDB/PostgreSQL, SQL e DML em lote, Redis, dados
CLOB/BLOB/JSON, observabilidade e o formato padronizado do relatório.

## Exemplo de prompt

```text
Analise o codebase Go localizado em <CAMINHO_DO_CODEBASE> usando integralmente o
roteiro em <CAMINHO_DESTE_PROJETO>/docs/go-application-inventory-guide.md.

Escopo: analise código Go, go.mod/go.sum, configurações, migrations, arquivos
SQL, testes, Dockerfiles, pipelines e manifests de entrega disponíveis no
repositório. Não acesse nem suponha informações de infraestrutura que não estejam
nesses artefatos.

Produza o relatório final estritamente no template Markdown definido na seção
"Consolidação e validação" do roteiro. Para cada achado, cite caminho relativo e
linha ou símbolo quando disponível, atribua confiança alta, média ou baixa e
separe claramente fatos, inferências, lacunas e perguntas em aberto.

Não exponha valores secretos. Se não houver evidência suficiente, registre uma
lacuna, os locais examinados e a evidência necessária para confirmar a conclusão.
```

## Saída esperada

O relatório inclui resumo e escopo, arquitetura, dependências, fluxos, integrações
técnicas e riscos. Se uma área não apresentar achados, o LLM deve declarar o
escopo e as evidências de busca, sem concluir que um comportamento não existe fora
do repositório.
