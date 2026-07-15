# Proposta: adicionar mapeamento de Redis ao roteiro de inventário Go

## Por quê

O roteiro atual orienta o mapeamento de Kafka e GaussDB/PostgreSQL, mas não
padroniza a investigação de Redis. Isso pode deixar sem rastreabilidade usos de
cache, sessões, filas, locks distribuídos, rate limiting e estruturas de dados
mantidas fora do banco relacional.

## O que muda

- Acrescentar ao roteiro uma seção específica para identificar e documentar o
  uso de Redis por aplicações Go.
- Cobrir bibliotecas clientes, versão, configuração de conexão, autenticação,
  TLS, timeouts, pool e ciclo de vida do cliente.
- Mapear cada uso por chave ou padrão de chave, estrutura de dados, comandos,
  TTL, fluxo funcional, serialização, invalidação e dependências entre cache e
  fonte de verdade.
- Registrar evidências de confiabilidade e segurança, incluindo tratamento de
  indisponibilidade, retries, consistência, locks, exposição de dados e riscos
  não comprovados.

## Impacto

- Capacidade existente modificada: `go-application-inventory-guide`.
- Alteração exclusivamente documental; não há mudança em runtime, APIs ou
  dependências de aplicações analisadas.
