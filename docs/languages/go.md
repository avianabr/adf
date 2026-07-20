# Perfil de linguagem: Go

Use este perfil com o [núcleo do roteiro](../application-inventory-guide.md)
quando o repositório contiver `go.mod`, `go.work` ou código Go relevante. Não
aplique estas convenções a componentes Java ou de outra linguagem.

## Descoberta e build

1. Leia `go.mod`, `go.sum` e `go.work` quando existirem. Registre módulo, versão
   Go, módulos do workspace, dependências diretas e substituições (`replace`).
2. Localize `package main`, `func main`, diretórios `cmd/`, `internal/`, `pkg/`,
   `api/`, `migrations/` e `testdata/`, sem assumir que a convenção determina o
   comportamento.
3. Relacione binários, `go build`, `go test`, Makefiles, scripts e pipelines ao
   módulo ou pacote compilado quando essa relação estiver explícita.
4. Trace `main`, inicialização, injeção de dependências, handlers, goroutines,
   jobs e o encerramento de clientes ou servidores.

## Dependências e componentes

1. Use `go.mod` para dependências diretas; use `go.sum` apenas para complementar
   versão ou evidência transitiva relevante.
2. Mapeie pacotes próprios e imports externos por finalidade. Identifique
   frameworks por chamadas concretas, como Gin, Echo, Fiber, gRPC, Cobra, GORM,
   sqlx ou similares.
3. Para integrações, procure APIs das bibliotecas usadas: por exemplo,
   `segmentio/kafka-go`, Sarama, `confluent-kafka-go` ou franz-go para Kafka;
   `database/sql`, pgx, pgxpool, GORM ou sqlx para banco; e `redis/go-redis` ou
   Redigo para Redis. A dependência declarada não prova uso efetivo.

## Testes e configuração

1. Localize arquivos `*_test.go`, tabelas de teste, mocks, fixtures e `testdata`.
2. Registre tags de build, variáveis de ambiente, arquivos de configuração,
   `embed`, geração de código e ferramentas declaradas em scripts ou módulos.
3. Cite pacote, arquivo, tipo, função ou método Go em cada achado específico.

| Item Go | Localização | Papel observado | Confiança |
|---|---|---|---|
| Módulo/workspace | `go.mod` ou `go.work` | Nome, versão e módulos | Alta |
| Executável | `cmd/.../main.go` ou outro `package main` | Ponto de entrada | Alta |
| Pacote | `<diretório>/*.go` | Responsabilidade e dependências | Média/Alta |

