# Roteiro guiado: inventário arquitetural e funcional de aplicações Go

Use este roteiro para analisar um codebase Go. Produza conclusões rastreáveis:
todo fato deve apontar para arquivo, pacote, símbolo, configuração ou teste. Não
trate convenções ou nomes como prova de comportamento; registre-os como hipótese
quando não houver evidência de execução ou teste.

## 1. Regras de trabalho

1. Trabalhe somente com o conteúdo disponível no repositório e artefatos de
   entrega associados.
2. Para cada achado, registre `evidência`, `confiança` (`alta`, `média` ou
   `baixa`) e `localização` (caminho e símbolo/linha, quando disponível).
3. Separe **fato**, **inferência**, **lacuna** e **pergunta em aberto**.
4. Nunca exponha segredos encontrados em arquivos de configuração; descreva apenas
   nome da variável, mecanismo de leitura e finalidade inferida.
5. Se SQL, tópicos ou tabelas forem construídos dinamicamente, registre a parte
   estática, os valores dinâmicos identificados e o que não foi possível provar.

## 2. Fase de descoberta

1. Liste a árvore relevante, ignorando artefatos gerados e dependências vendorizadas
   quando não forem fonte de comportamento próprio.
2. Leia `go.mod`, `go.sum`, `go.work` (se houver), `README`, `Makefile`, arquivos
   de CI/CD, Dockerfiles, Helm/Kubernetes e configurações de ambiente.
3. Identifique módulos, binários (`package main`), comandos, pontos de entrada,
   pacotes `internal`, `pkg`, `api`, `cmd`, `migrations` e `testdata`.
4. Trace do ponto de entrada para inicialização, injeção de dependências, handlers,
   jobs e encerramento da aplicação.

Entregue uma tabela inicial:

| Item | Localização | Papel observado | Confiança |
|---|---|---|---|
| Módulo Go | `go.mod` | Nome e versão do módulo | Alta |
| Executável/comando | `cmd/.../main.go` | Ponto de entrada | Alta |
| Configuração | `...` | Fontes e chaves lidas | Média/Alta |

## 3. Inventário de dependências, pacotes e frameworks

1. Extraia dependências diretas de `go.mod`; use `go.sum` apenas para complementar
   versões ou dependências transitivas relevantes.
2. Agrupe imports externos por finalidade: HTTP/RPC, configuração, DI, logs,
   métricas, tracing, autenticação, persistência, mensageria, serialização e testes.
3. Liste todos os pacotes próprios e sua responsabilidade, consumidores e
   dependências de saída.
4. Identifique frameworks por uso concreto de APIs (não apenas pela presença no
   módulo), como Gin, Echo, Fiber, gRPC, Cobra, GORM, sqlx ou similares.
5. Destaque explicitamente: drivers SQL, ORMs/query builders, bibliotecas Kafka,
   clientes Redis e bibliotecas de serialização de mensagens.

| Dependência/pacote | Versão | Categoria | Uso concreto e localização | Confiança |
|---|---|---|---|---|

## 4. Mapa arquitetural

Para cada componente, descreva responsabilidade, entradas, saídas, dependências,
dados manipulados e falhas relevantes. Cubra:

- bordas de entrada: HTTP, gRPC, CLI, cron, filas, Kafka;
- casos de uso/serviços e regras de negócio;
- adaptadores de persistência, cache e integrações externas;
- configuração, feature flags e gestão de segredos;
- logging, métricas, tracing, health checks e tratamento de erro;
- autenticação, autorização, validação e proteção de dados;
- build, testes, imagem, deploy e execução operacional.

Inclua um diagrama textual conciso:

```text
[Entrada] -> [handler/consumer] -> [caso de uso] -> [repositório/cliente]
                                               -> [efeito: DB/Kafka/API]
```

Use apenas setas comprovadas por chamadas, injeção de dependência ou configuração.

## 5. Mapa funcional

Derive capacidades de handlers, comandos, consumidores, serviços, modelos e testes.
Para cada capacidade, informe:

| Capacidade | Ator/gatilho | Pré-condições | Etapas | Dados/efeitos | Falhas | Evidência |
|---|---|---|---|---|---|---|

Descreva o comportamento, não apenas a estrutura técnica. Caso o nome de domínio
seja ambíguo, use uma descrição neutra e registre a ambiguidade como pergunta.

## 6. Roteiro específico: Kafka

1. Localize imports e configuração de clientes, por exemplo `segmentio/kafka-go`,
   `Shopify/IBM/sarama`, `confluent-kafka-go`, `franz-go` ou wrappers internos.
2. Identifique versão, pacote que encapsula o cliente e como brokers, TLS, SASL,
   timeouts e credenciais são fornecidos (sem revelar valores secretos).
3. Para cada produtor, registre tópico, chave, partição quando explícita, headers,
   schema/formato, serialização, confirmação, retries, timeout e fluxo funcional
   que produz o evento.
4. Para cada consumidor, registre tópico(s), grupo, estratégia de consumo,
   desserialização, handler, commit/ack, paralelismo, retries, DLQ e efeitos
   persistentes ou externos.
5. Procure garantias e riscos: duplicidade/idempotência, ordenação, reprocessamento,
   poison messages, transações/outbox, observabilidade e desligamento seguro.

| Papel | Pacote/símbolo | Biblioteca/versão | Tópico | Grupo | Contrato | Fluxo | Confiabilidade | Evidência |
|---|---|---|---|---|---|---|---|---|

Se tópico, contrato ou grupo vier de configuração, cite a chave e seus locais de
uso. Não infira "exactly once" sem configuração e código que o comprovem.

## 7. Roteiro específico: GaussDB/PostgreSQL

1. Localize DSNs, variáveis de ambiente, fábrica de conexões e pool. Identifique
   driver e biblioteca: `database/sql` com `lib/pq`, `pgx`, `pgxpool`, GORM, sqlx,
   SQLC ou outra.
2. Mapeie o ciclo de vida do pool: abertura, limites, timeouts, health check e
   encerramento.
3. Localize migrations, DDL, schemas, tabelas, visões, índices, funções e
   procedimentos; relacione-os aos repositórios e casos de uso.
4. Identifique transações: início, propagação de contexto, isolamento quando
   explícito, commit, rollback e operações agrupadas.
5. Diferencie evidência de PostgreSQL, GaussDB e compatibilidade apenas assumida.
   Não conclua compatibilidade sem documentação, configuração ou teste no repo.
6. Localize sequências e colunas com valores gerados automaticamente em DDL,
   migrations, queries, configurações e metadados de ORM. Registre somente os
   mecanismos observados, como `SERIAL`, `BIGSERIAL`, `IDENTITY`,
   `DEFAULT nextval(...)` ou equivalentes comprovados.
7. Para cada sequência ou geração automática, relacione o recurso à tabela e
   coluna, tipo e local de definição ou alteração. Registre parâmetros
   observáveis — valor inicial, incremento, mínimo, máximo e ciclo — sem supor
   valores que não estejam disponíveis.
8. Rastreie como a aplicação recebe ou usa o valor gerado: cláusula `RETURNING`,
   leitura explícita da sequência, preenchimento pelo driver ou comportamento de
   ORM. Classifique como hipótese ou lacuna qualquer relação não comprovada, bem
   como garantias de unicidade, tratamento de overflow ou semântica de geração.
9. Para cada function ou procedure definida em DDL, migration ou schema,
   diferencie seu tipo e registre nome qualificado, assinatura, linguagem,
   parâmetros, retorno quando aplicável, objetos afetados e a localização da
   definição ou alteração. Não trate a definição como prova de que a rotina é
   chamada pela aplicação.
10. Localize chamadas a functions e procedures em SQL, query builders, drivers e
    ORMs, como `SELECT` e `CALL`. Relacione cada chamada comprovada ao arquivo,
    pacote ou símbolo Go responsável e ao fluxo funcional, indicando os
    parâmetros e resultados observáveis.
11. Registre evidências sobre transação, tratamento de erros, permissões e
    efeitos colaterais de cada chamada ou rotina. Classifique como hipótese ou
    lacuna qualquer assinatura, efeito, garantia transacional, permissão ou
    invocação que não possa ser comprovada pelo codebase ou configuração
    disponível.

| Recurso | Banco/tipo | Tabela/coluna, sequência ou rotina | Assinatura/operação | Pacote/símbolo Go | Transação/erros | Fluxos | Evidência |
|---|---|---|---|---|---|---|---|

## 8. Inventário de SQL e DML

Localize SQL literal, arquivos `.sql`, queries geradas, query builders, chamadas de
ORM e SQL dinâmico. Para cada operação `SELECT`, `INSERT`, `UPDATE`, `DELETE`,
`MERGE` ou equivalente, gere uma linha:

| ID | Operação | Origem (arquivo/símbolo) | Tabelas/visões | Parâmetros | Transação | Fluxo funcional | Complexidade | Evidência |
|---|---|---|---|---|---|---|---|---|

Inclua uma versão resumida do comando que preserve tabelas, junções, filtros e
efeitos. Para builders/ORMs, descreva a operação gerada somente no nível provado
pela chamada; não invente SQL final.

### DML em lote

1. Localize operações em lote, especialmente `INSERT`, `MERGE` e equivalentes
   gerados por driver, ORM ou query builder. Diferencie um comando único com
   múltiplos valores, execução repetida em transação, APIs de batch e outros
   mecanismos apenas quando o código ou a biblioteca utilizada o comprovar.
2. Rastreie como cada lote é formado: fonte dos dados, coleção ou stream de
   entrada, transformação, agrupamento, condição de divisão e configuração
   relevante. Registre a quantidade de registros por lote, seu limite ou critério
   de tamanho somente quando observável; não a deduza de convenções.
3. Para cada lote, registre os comandos ou chamadas executados, tabelas ou visões
   afetadas, parâmetros, pacote/símbolo responsável e fluxo funcional. Quando o
   SQL for dinâmico, preserve a parte estática e indique o que não foi possível
   determinar.
4. Mapeie a fronteira transacional e a estratégia de commit: início e término da
   transação, commit por lote, commit ao final ou outro ponto comprovado. Indique
   também se um lote pode compartilhar transação com outros passos.
5. Registre o tratamento de exceções: erros propagados ou tratados, rollback,
   retry, compensação e possibilidade de resultado parcial. Classifique como
   hipótese ou lacuna qualquer tamanho de lote, atomicidade, política de commit,
   recuperação ou comportamento de erro sem evidência no codebase ou na
   configuração disponível.

| ID/lote | Operação e mecanismo | Formação e origem dos dados | Tamanho/critério | Origem Go | Tabelas/comandos | Transação/commit | Erro/rollback/retry | Fluxo/evidência |
|---|---|---|---|---|---|---|---|---|

### Índice de complexidade SQL

| Índice | Critério |
|---|---|
| 1 — simples | Uma tabela e operação direta, sem junção, subconsulta ou agregação. |
| 2 — moderada | Filtros, ordenação, paginação, `IN` ou agregação simples. |
| 3 — composta | Múltiplas tabelas, junção, CTE ou subconsulta. |
| 4 — avançada | Múltiplas CTEs/subconsultas, funções de janela, `MERGE`, lote ou lógica condicional relevante. |
| 5 — crítica | SQL dinâmico complexo, procedimentos/funções, múltiplas etapas dependentes, alto volume potencial ou semântica transacional difícil de verificar. |

Registre os critérios observados junto do índice. O índice mede complexidade de
leitura/manutenção e risco técnico aparente; não é uma medição de performance.

## 9. Roteiro específico: Redis

1. Localize imports, wrappers internos e configuração de clientes Redis, como
   `redis/go-redis`, `gomodule/redigo` ou outra biblioteca. Registre versão,
   endereços ou sentinelas, banco lógico, credenciais, TLS, timeouts e origem de
   cada configuração, sem expor valores secretos.
2. Mapeie o ciclo de vida do cliente e do pool: criação, limites, health check,
   instrumentação e encerramento. Diferencie cliente Redis único, Sentinel e
   Cluster apenas quando isso estiver comprovado por configuração ou código.
3. Para cada uso, identifique o papel comprovado — cache, sessão, fila, lock,
   rate limiting ou outro — e registre pacote/símbolo, padrão de chave, estrutura
   Redis (`string`, hash, lista, conjunto, sorted set, stream ou outra), comandos
   executados e fluxo funcional associado.
4. Registre formato e serialização do valor, TTL/expiração, política de
   invalidação, namespace e fonte de verdade. Não suponha que Redis seja apenas
   cache ou que uma escrita seja persistente sem evidência.
5. Procure evidências de indisponibilidade e consistência: timeouts, retries,
   fallback, degradação, operações atômicas, concorrência, locks, idempotência,
   duplicidade em filas, limites de memória e tratamento de dados sensíveis.

| Papel | Pacote/símbolo | Biblioteca/versão | Chave/padrão | Estrutura e comandos | TTL/invalidação | Fluxo | Riscos/evidência |
|---|---|---|---|---|---|---|---|

Caso uma chave, TTL ou comando seja montado dinamicamente, registre a parte
estática, os valores dinâmicos identificados e o que não pôde ser determinado.
Classifique como hipótese ou lacuna toda garantia de cache, lock, entrega de fila,
consistência ou segurança que não seja comprovada pelo codebase ou configuração
disponível.

## 10. Tipos CLOB, BLOB e JSON

Procure DDL, migrations, structs, tags, `Scan`/`Value`, serializadores, uploads e
downloads, queries e contratos externos. Mapeie CLOB/BLOB e equivalentes efetivos
do banco (por exemplo, `text`, `bytea`, `json` e `jsonb` no PostgreSQL) sem assumir
equivalência sem evidência.

| Tipo/coluna | Tipo no banco | Representação Go | Leitura/escrita | Conversão/serialização | Fluxo exposto | Riscos/evidência |
|---|---|---|---|---|---|---|

Verifique e registre, quando observável: streaming versus carga integral em
memória, limites de tamanho, encoding, validação de JSON, versionamento de schema,
sanitização, criptografia, retenção e exposição em logs/respostas.

## 11. Roteiro específico: observabilidade

1. Localize imports, wrappers internos, inicialização e configuração de logs,
   métricas, tracing e telemetria, como `log/slog`, Zap, Logrus, Prometheus,
   OpenTelemetry ou bibliotecas equivalentes. Registre versão quando disponível,
   mas não trate uma dependência declarada como instrumentação efetivamente usada.
2. Mapeie criação, injeção, propagação de contexto e encerramento dos componentes
   de observabilidade. Identifique configurações de nível, formato, destino,
   exportador, endpoint, protocolo, credenciais, batching e amostragem sem expor
   valores secretos.
3. Para cada componente ou fluxo relevante, inventarie os sinais observáveis:
   eventos e níveis de log, campos estruturados, contadores, gauges, histogramas,
   spans, atributos, eventos de span e identificadores de correlação. Relacione
   cada sinal ao pacote/símbolo e ao fluxo funcional ou operacional comprovado.
4. Procure instrumentação em bordas de entrada e saída — HTTP, gRPC, jobs,
   consumidores, banco, cache e chamadas externas — e registre cobertura de
   sucesso, erro, latência e dependências somente quando observável.
5. Registre evidências sobre falhas de instrumentação ou exportação, retries,
   buffering, perda e degradação de telemetria. Verifique também mascaramento,
   filtragem ou exposição de dados sensíveis em logs e atributos. Classifique como
   hipótese ou lacuna qualquer garantia de cobertura, confiabilidade, retenção,
   amostragem ou proteção de dados que não seja comprovada pelo codebase ou pela
   configuração disponível.

| Sinal | Pacote/símbolo | Biblioteca/versão | Evento, métrica ou span | Atributos/correlação | Configuração/destino | Fluxo/cobertura | Riscos/evidência |
|---|---|---|---|---|---|---|---|

## 12. Consolidação e validação

Produza o relatório final estritamente em Markdown, usando o template abaixo. Não
omita uma seção: quando não houver achados, use o formato de seção sem achados
definido ao final. Preserve caminhos relativos ao repositório e acrescente linha
ou símbolo quando disponível.

### Convenções obrigatórias

Use estes blocos para conclusões que não couberem naturalmente em uma tabela:

```markdown
- **Fato:** conclusão diretamente observada.
  - **Confiança:** alta
  - **Evidência:** `caminho/arquivo.go:linha` — pacote, símbolo, configuração ou teste.

- **Inferência:** conclusão derivada de evidências, com a justificativa.
  - **Confiança:** média
  - **Evidência:** `caminho/arquivo.go:símbolo` — por que a evidência a sustenta.

- **Lacuna:** comportamento relevante que não pôde ser provado.
  - **Evidência disponível:** locais verificados.
  - **Para confirmar:** arquivo, configuração, teste ou documentação necessária.

- **Pergunta em aberto:** decisão ou contexto externo necessário.
  - **Motivo:** por que o codebase não a responde.
```

Use `alta`, `média` ou `baixa` em toda confiança. Não exponha segredos; cite
apenas nome da variável, mecanismo de leitura e finalidade inferida.

### Template do relatório final

```markdown
# Inventário da aplicação Go: <nome ou módulo>

## 1. Resumo executivo

- **Escopo analisado:** <diretórios, revisão/branch se disponível e artefatos lidos>.
- **Objetivo aparente:** <fato ou inferência identificada>.
- **Pontos principais:** <3–7 achados, riscos ou lacunas priorizados>.

## 2. Escopo e método

| Item | Cobertura ou critério | Evidência |
|---|---|---|
| Repositório/módulo | <módulo e raiz analisada> | `go.mod` |
| Fontes consultadas | <código, configs, migrations, testes etc.> | `<caminhos>` |
| Limites da análise | <itens indisponíveis ou fora do escopo> | <evidência> |

## 3. Arquitetura e componentes

<Diagrama textual das relações comprovadas.>

| Componente | Responsabilidade | Entradas/saídas | Dependências | Falhas/riscos | Evidência |
|---|---|---|---|---|---|

## 4. Dependências, pacotes e frameworks

| Dependência/pacote | Versão | Categoria | Uso concreto | Evidência |
|---|---|---|---|---|

## 5. Capacidades e fluxos funcionais

| Capacidade | Ator/gatilho | Pré-condições | Etapas | Dados/efeitos | Falhas | Confiança | Evidência |
|---|---|---|---|---|---|---|---|

## 6. Integrações Kafka

| Papel | Pacote/símbolo | Biblioteca/versão | Tópico/grupo | Contrato | Fluxo | Confiabilidade | Evidência |
|---|---|---|---|---|---|---|---|

## 7. Persistência GaussDB/PostgreSQL

| Recurso | Banco/tipo | Tabela/coluna, sequência ou rotina | Assinatura/operação | Origem Go | Transação/erros | Fluxo | Evidência |
|---|---|---|---|---|---|---|---|

## 8. SQL e DML

| ID | Operação | Origem | Tabelas/visões | Parâmetros | Transação | Fluxo | Complexidade | Evidência |
|---|---|---|---|---|---|---|---|---|

### DML em lote

| ID/lote | Operação/mecanismo | Formação/origem | Tamanho/critério | Origem Go | Transação/commit | Erro/rollback/retry | Evidência |
|---|---|---|---|---|---|---|---|

## 9. Integrações Redis

| Papel | Pacote/símbolo | Biblioteca/versão | Chave/padrão | Estrutura/comandos | TTL/invalidação | Fluxo | Riscos/evidência |
|---|---|---|---|---|---|---|---|

## 10. CLOB, BLOB e JSON

| Tipo/coluna | Tipo no banco | Representação Go | Leitura/escrita | Conversão | Fluxo exposto | Riscos/evidência |
|---|---|---|---|---|---|---|

## 11. Observabilidade

| Sinal | Pacote/símbolo | Biblioteca/versão | Evento, métrica ou span | Atributos/correlação | Destino | Cobertura | Riscos/evidência |
|---|---|---|---|---|---|---|---|

## 12. Riscos, lacunas, hipóteses e perguntas em aberto

| Prioridade | Tipo | Descrição | Impacto | Evidência disponível | Próxima evidência/ação |
|---|---|---|---|---|---|
```

Após cada tabela, acrescente blocos de **Fato**, **Inferência**, **Lacuna** ou
**Pergunta em aberto** quando forem necessários para explicar um item. Não repita
o conteúdo da tabela sem acrescentar contexto verificável. Para uma seção sem
achados, escreva:

```markdown
> **Sem achados no escopo analisado.** Foram verificados <caminhos e padrões de
> busca>; isso não comprova ausência de comportamento em infraestrutura externa.
```

Antes de finalizar, confirme que todas as seções foram preenchidas ou declaradas
sem achados, que cada item relevante tem evidência, que cada inferência está
sinalizada e que nenhuma ausência de código foi apresentada como ausência de
comportamento em infraestrutura externa.
