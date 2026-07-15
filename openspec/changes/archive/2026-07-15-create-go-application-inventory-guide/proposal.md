# Proposta: criar roteiro de inventário de aplicações Go

## Por quê

Avaliações de codebases Go costumam depender de conhecimento tácito e de leituras
manuais pouco consistentes. Um roteiro guiado permite que um LLM examine uma
aplicação de forma repetível, separando o que é observável no código de
inferências, lacunas e riscos.

## O que muda

- Adicionar um roteiro em Markdown para inventário assistido por LLM de aplicações
  escritas em Go.
- Cobrir duas perspectivas complementares: arquitetural (estrutura, dependências,
  fronteiras, dados, operações e qualidade) e funcional (capacidades, atores,
  fluxos, interfaces e regras de negócio).
- Incluir roteiros específicos para mapear o uso de Kafka e de GaussDB/PostgreSQL,
  desde as bibliotecas e configuração até os fluxos, contratos, dados e falhas
  associados.
- Inventariar dependências, pacotes e frameworks Go, destacando o driver de acesso
  ao banco de dados e as bibliotecas clientes usadas para produzir ou consumir
  eventos Kafka.
- Mapear consultas SQL e operações DML executadas pela aplicação, com um índice
  consistente de complexidade por comando.
- Rastrear o uso de tipos de dados CLOB, BLOB e JSON entre modelos Go, parâmetros,
  consultas, serialização e fluxos funcionais.
- Definir uma sequência de investigação, evidências mínimas, formato de saída e
  critérios para explicitar incertezas.

## Impacto

- Nova capacidade: `go-application-inventory-guide`.
- Sem mudança de runtime, APIs, dependências ou comportamento de aplicações.
- O roteiro será aplicável a repositórios Go monolíticos, serviços e CLIs; os
  achados devem sempre referenciar caminhos e símbolos do codebase analisado.
