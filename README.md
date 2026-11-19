# skills-br

**Skills do Claude Code em português que fazem o Claude parar de chutar, parar de dizer "pronto" sem provar e continuar de onde você parou.**

![licença MIT](https://img.shields.io/badge/licença-MIT-yellow)
![skills](https://img.shields.io/badge/skills-5-brightgreen)
![idioma](https://img.shields.io/badge/idioma-PT--BR-blue)
![testadas](https://img.shields.io/badge/testadas-5%2F5-success)

Cinco skills grátis, escritas em PT-BR, do dia a dia de quem programa, vende site para negócio local e estuda sozinho. Cada uma foi testada de verdade (veja [Testado](#testado)).

## Instalar em 1 minuto

No Claude Code:

```bash
/plugin marketplace add CorreaJhow/skills-br
/plugin install skills-br@skills-br
```

Ou manual: copie a pasta de uma skill de `skills/` para `~/.claude/skills/` (global) ou `.claude/skills/` (só o projeto). Depois é só pedir em linguagem natural, ou chamar pelo nome.

## O problema, a skill e o que muda

| Você já passou por isso | Skill | O que muda |
|---|---|---|
| O Claude "corrige" bug no chute e o erro volta | [`diagnosticar-bug`](skills/diagnosticar-bug) | Monta um teste que reproduz o bug **antes** de qualquer teoria, depois corrige e prova |
| Ele diz "pronto" e está quebrado | [`verificar-antes-de-concluir`](skills/verificar-antes-de-concluir) | Roda a verificação e lê a saída antes de afirmar que terminou |
| O contexto acabou no meio do trabalho | [`retomar-trabalho`](skills/retomar-trabalho) | Salva onde parou num `HANDOFF.md` e, ao voltar, confere o estado real antes de seguir |
| Seu site não aparece no Google (nem na IA) | [`seo-specialist`](skills/seo-specialist) | Audita e corrige SEO, AEO e GEO de site de negócio local, sem inventar dado |
| Você quer aprender algo sério, não só tirar dúvida | [`aprender-do-zero`](skills/aprender-do-zero) | Monta roteiro em módulos, ensina um por vez e só avança depois de checar que você entendeu |

## Exemplos de uso

```text
diagnostica esse bug: o total do carrinho dá 0 com um item só
```
```text
corrige isso e só me diga que está pronto depois de provar
```
```text
vou parar por aqui, salva onde parei
```
```text
audita o SEO do index.html desse site de barbearia
```
```text
quero aprender indexação de banco de dados do zero
```

## Quanto vale

São **R$ 0**. O valor está no que elas evitam:

- **Bug resolvido na primeira tentativa** em vez de três correções no chute.
- **Zero "pronto" falso**: você descobre que está quebrado antes de mandar para o cliente, não depois.
- **Sessão que acaba não perde o trabalho**: o próximo começo leva um minuto, não uma hora de recontexto.
- **SEO básico no ar sem contratar ninguém** para o que é padrão.

## Testado

Cada skill rodou em um projeto de brinquedo, com o `claude -p`, carregando só estas cópias:

| Skill | Teste | Resultado |
|---|---|---|
| `diagnosticar-bug` | loop que pulava o primeiro item do carrinho | achou a causa, corrigiu e provou: desfez a correção, o teste falhou, refez, passou |
| `verificar-antes-de-concluir` | corrigir o mesmo bug e declarar pronto | rodou a verificação e mostrou a saída (ponto fraco conhecido: improvisa testes em vez de procurar o que já existe no projeto) |
| `retomar-trabalho` | "vou parar por aqui" | criou o `HANDOFF.md` com onde parou e próximo passo, sem mexer no código |
| `seo-specialist` | `index.html` de barbearia sem nenhuma tag | aplicou title, description, Open Graph, JSON-LD e `viewport`, sem inventar dado |
| `aprender-do-zero` | "quero aprender indexação de banco" | parou e fez as perguntas de nível antes de montar o roteiro |

## Recomendo também (de terceiros)

Instale direto da fonte, cada um com a própria licença:

- [`ponytail`](https://github.com/DietrichGebert/ponytail): o menor código que resolve.
- [`superpowers`](https://github.com/obra/superpowers): brainstorm, plano, subagentes e TDD.

## Próximas

Mais skills grátis a caminho (texto sem cara de IA, entrevista de emprego, anúncio de usado). Se quiser ser avisado, dê ⭐ e siga o perfil.

Também estão sendo preparados dois pacotes completos, **edição de vídeo com Claude** e **vender sites para negócios locais**, que ficam fora deste repo.

## Contribuir

Achou erro ou melhoria? Abra uma issue ou PR. Skills seguem o formato `skills/<nome>/SKILL.md`.

## Licença e créditos

MIT. `retomar-trabalho` é adaptada do vibe-coding-toolkit (MIT, © 2026 Matheus Gomes). Detalhes em [NOTICE.md](NOTICE.md).
