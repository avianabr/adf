## ADDED Requirements

### Requirement: Mapeamento de Redis

O roteiro SHALL orientar o LLM a identificar e documentar o uso de Redis pela
aplicação, incluindo biblioteca cliente, configuração de conexão, credenciais,
TLS, pool, estruturas de dados, chaves, comandos, TTLs e fluxos funcionais.

#### Scenario: Aplicação usa Redis

- **WHEN** importações, configurações ou código indicarem integração com Redis
- **THEN** o relatório SHALL identificar a biblioteca utilizada e sua versão
  quando disponível
- **AND** SHALL mapear cada uso para cache, sessão, fila, lock, rate limiting ou
  outro papel comprovado, com pacote ou símbolo responsável
- **AND** SHALL registrar padrões de chave, tipo de estrutura Redis, comandos,
  serialização, TTL e estratégia de invalidação quando observáveis
- **AND** SHALL relacionar o uso aos fluxos funcionais e à fonte de verdade dos
  dados, quando essa relação puder ser comprovada.

#### Scenario: Confiabilidade e segurança de Redis analisadas

- **WHEN** o LLM analisa uma integração Redis
- **THEN** o relatório SHALL registrar evidências sobre autenticação, TLS,
  timeouts, pool, tratamento de indisponibilidade, retries e degradação
- **AND** SHALL registrar evidências sobre consistência, expiração, concorrência,
  locks, filas, dados sensíveis e exposição em logs ou interfaces
- **AND** SHALL classificar como lacuna qualquer garantia ou comportamento que
  não possa ser comprovado pelo codebase ou por sua configuração disponível.
