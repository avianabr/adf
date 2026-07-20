# Proposta: tornar o roteiro modular e adicionar perfil Java

## Por quê

O roteiro atual é dedicado a aplicações Go: sua descoberta, dependências,
estrutura de código e exemplos de prompt dependem de `go.mod` e convenções Go.
Adicionar novas linguagens diretamente ao mesmo documento tornaria a análise
ambígua e difícil de manter. É necessário separar as regras compartilhadas dos
detalhes de cada linguagem.

## O que muda

- Reorganizar o roteiro em um núcleo comum, independente de linguagem, e perfis
  selecionáveis por linguagem.
- Preservar a cobertura atual de Go como perfil próprio, sem remover os
  requisitos de investigação existentes.
- Adicionar Java como o primeiro perfil adicional, abrangendo JDK, Maven/Gradle,
  estrutura de fontes e recursos, pontos de entrada, frameworks, dependências,
  testes e artefatos de build.
- Atualizar o README e os prompts de exemplo para escolher o perfil adequado e
  combinar o núcleo com um ou mais perfis, sem aplicar convenções de uma linguagem
  a outra.

## Impacto

- Capacidade existente modificada: `go-application-inventory-guide`.
- Novo material documental para o perfil Java e para a seleção de perfis.
- Alteração exclusivamente documental; não há mudança em runtime, APIs ou
  dependências de aplicações analisadas.
