---
name: retomar-trabalho
description: Use quando um trabalho de código ou de cliente vai ficar pela metade e continuar em outra sessão ("para por aqui", "continua amanhã", "salva onde parou", contexto acabando), ou quando o usuário pedir pra retomar algo ("de onde paramos?", "continua o X") — escreve ou lê o HANDOFF.md e confere o estado real antes de seguir.
---

# Retomar trabalho

Adaptado de `templates/task-handoff.md.template` do vibe-coding-toolkit (soumatheusgomes/vibe-coding-toolkit, commit `7ef68dd`, MIT, © 2026 Matheus Gomes).

**Regra:** o handoff é contexto, não prova. Ao retomar, confira arquivos, git e checks antes de confiar no que está escrito.

## Onde fica
- `HANDOFF.md` na raiz do projeto ou na pasta do cliente (`clientes/<nome>/`).
- Um só por projeto. Se já existe, atualize; não crie outro. Se o projeto já tem plano ou registro de tarefa (plano do Superpowers, issue), use ele.
- Decisão que vale pra sempre vai pro `decisoes.md`/`CLAUDE.md` do projeto, não pro handoff.
- Cliente PJ: registre também uma linha no `## Histórico` do `README.md` (`- AAAA-MM-DD (tipo): texto`), que é o que a Central lê.
- Terminou o trabalho? **Apague o `HANDOFF.md`.** Handoff velho engana a próxima sessão.

## Ao pausar: escrever
Rode `git status` e os checks relevantes **agora** e preencha:

```markdown
# Handoff — <tarefa>
- **Objetivo e aceite:** <o que foi pedido e como saber que terminou>
- **Estado conferido:** <AAAA-MM-DD HH:MM, branch/commit, mudanças locais (nunca suponha árvore limpa)>
- **Feito:** <mudanças e arquivos>
- **Evidência:** <comandos rodados, resultado e quando; o que falhou e o que não foi rodado>
- **Falta:** <menor próximo passo, dependências, riscos conhecidos>
- **Bloqueios:** <causa, o que depende disso, condição pra destravar>
- **Recursos abertos:** <servidor rodando, porta, banco temporário, build; o que precisa limpar>
- **Revisitar:** <fontes ou suposições que podem ter mudado (resposta do cliente, versão de lib)>
```

Nunca coloque senha, token, chave de API, dado pessoal de cliente nem log inteiro.

## Ao retomar: conferir antes de seguir
1. Leia o `HANDOFF.md` (e o `README.md` do cliente, se houver).
2. Confira o estado real: `git status`, `git log -5 --oneline`, os arquivos citados em "Feito" existem e têm o que diz.
3. Rode de novo os checks da "Evidência". Resultado diferente do anotado? Vale o de agora; avise o usuário.
4. Confira "Recursos abertos": processo ou porta que ainda está ocupado, ou que morreu.
5. Diga em 2-3 linhas onde parou e qual o próximo passo, e siga a partir de "Falta".
