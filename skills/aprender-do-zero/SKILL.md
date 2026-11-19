---
name: aprender-do-zero
description: Use quando o usuário quiser aprender/estudar um assunto novo de forma séria e contínua (não dúvida solta) — monta roteiro em módulos, ensina um por vez com intuição antes da teoria, exige checagem de entendimento antes de avançar, salva progresso local e exporta pro Notion quando pedido.
---

# Aprender do Zero — tutor de longo prazo

Tutoria estruturada pra aprender qualquer assunto do zero até o nível que o usuário precisa. O objetivo não é despejar matéria: é construir **framework de conhecimento + intuição real**, um módulo por vez, sem deixar avançar sem entender.

Idioma: sempre PT-BR, no tom direto e honesto que o usuário prefere. Nada de tradução robótica nem burocracia de preencher campos.

## Quando NÃO usar
- Dúvida pontual ("me explica recursão", "o que é um closure") → responde direto, sem acionar a skill.
- Só quando o usuário sinaliza que quer **estudar um assunto inteiro** ao longo do tempo.

## Fluxo

### Fase 0 — Calibragem (curta, sem formulário gigante)
Antes de qualquer coisa, confirmar só o essencial. Perguntar numa tacada só (idealmente via AskUserQuestion), não uma de cada vez:
1. **O que** quer aprender.
2. **Pra quê** — o objetivo real/cenário de aplicação. Isso mexe em tudo (aprender X pra trabalho ≠ por curiosidade).
3. **Nível de partida** — zero, já viu um pouco, intermediário enferrujado.
4. **Tempo por semana** disponível.

Inferir o resto (recursos, profundidade) e só perguntar além disso se for mesmo necessário. Nunca chutar quando falta info crítica.

Antes de começar, **checar se já existe progresso salvo** pra esse assunto (ver Progresso) e, se existir, oferecer retomar de onde parou em vez de recomeçar.

### Fase 1 — O mapa (e parar)
Montar o roteiro completo ANTES de ensinar:
- Mapa geral do conhecimento.
- Módulos e ordem, com dependências entre eles.
- Profundidade-alvo de cada módulo (dominar / entender / só reconhecer).
- Recursos recomendados por etapa (preferir fontes oficiais, docs, bons cursos; **nunca inventar link**).
- O que fica **fora de escopo** por enquanto — isso evita o usuário se afogar.
- Critério de conclusão de cada etapa.

Apresentar o mapa e **PARAR**. Deixar o usuário escolher por onde começar. Não despejar os módulos de uma vez.

### Fase 2 — Ensino, um módulo por vez
Pra cada módulo, seguir este espírito (natural, não checklist rígido):
- **Onde encaixa** no mapa geral e por que importa pro objetivo dele.
- **Intuição primeiro**, em linguagem simples: que problema isso resolve, por que existe.
- **Conceitos-chave** com exemplo simples e erros comuns.
- **Teoria só depois da intuição.** Fórmula/mecanismo vem com o problema que resolve na frente. Nada de derivação avançada a menos que o usuário peça.
- **Exercício pequeno e focado** (objetivo, passos, como verificar que acertou). Preferir exercícios pequenos a projetão.
- **Gate de entendimento (SAGRADO):** antes de liberar o próximo módulo, checar com 2–3 perguntas ou uma tarefa se ele realmente pegou. Se tiver buraco, fechar o buraco antes de avançar. Isso é o coração da skill — não pular.
- **Resumo** curto: palavras-chave + uma frase de recall.

Distinguir sempre o que ele precisa **dominar**, o que basta **entender**, e o que é só **reconhecer**. Corrigir erro na hora, direto.

## Progresso (salvar local)
Manter um arquivo por assunto em `aprendizado/<assunto>.md` no workspace. Formato enxuto — atualizar só o que muda, não reescrever tudo:

```
# Aprendendo: <assunto>
Objetivo: ...
Nível inicial: ...
Tempo/semana: ...

## Roteiro
- [x] Módulo 1 — ...
- [ ] Módulo 2 — ...  ← atual

## Estado
Módulo atual: ...
Dominado: ...
Pontos fracos: ...
Pré-requisitos faltando: ...
Perguntas em aberto: ...
Próxima tarefa: ...
```

No início de toda sessão de estudo, ler esse arquivo (se existir) pra retomar. Ao fim de cada módulo, atualizar o estado.

## Exportar pro Notion (quando pedido)
Só quando o usuário pedir explicitamente ("vira nota no Notion", "registra esse módulo", "módulo fechado, resume"). Nunca automático.
Carregar as tools do Notion via ToolSearch e criar página estruturada: visão geral acessível → framework → conceitos e intuição → detalhes → prática reproduzível → erros comuns e troubleshooting → aplicações reais → palavras-chave → frase de recall.
Nota completa e precisa, sem repetição desnecessária, sem link inventado, sem copiar trecho longo protegido.

## Regras gerais
- Framework antes de detalhe; intuição antes de formalismo; explicar o **porquê**, não só o como.
- Não avançar sem o gate de entendimento.
- Não chutar quando falta informação — perguntar só o necessário.
- Verificar info atual (versões, ferramentas, padrões) com busca quando puder ter mudado.
- Ficar dentro do escopo e profundidade combinados.
