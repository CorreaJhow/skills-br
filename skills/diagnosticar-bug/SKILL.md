---
name: "diagnosticar-bug"
description: "Use quando algo quebrou, dá erro, falha ou ficou lento (site de cliente, código do serviço) e a causa não é óbvia: monta um teste que reproduz o bug antes de qualquer teoria, depois isola, levanta hipóteses, corrige e limpa."
---

# Diagnosticar bug

Disciplina para bug difícil. Adaptado de `diagnosing-bugs` em mattpocock/skills (MIT, © 2026 Matt Pocock), com rastreio da causa, defesa em profundidade e a regra das 3 tentativas do `systematic-debugging` do Superpowers (obra/superpowers, MIT). No perfil **grande**, o `superpowers:systematic-debugging` assume; a Fase 1 daqui (ciclo apertado) continua sendo o padrão de qualidade. Pule uma fase só com justificativa explícita. Para erro de digitação ou bug óbvio, corrija direto.

## Antes de tudo: esconder segredo
Esta skill mostra comandos, saídas e logs. **Troque todo segredo por `<REDACTED>`** antes de mostrar. Monte os testes lendo credenciais de variável de ambiente, nunca colando no comando. Log capturado carrega header de autenticação: cite só as linhas que importam. Se o texto censurado não bastar para diagnosticar, diga e pergunte.

## Fase 1: montar o ciclo de verificação (esta é a skill)
O resto é mecânico. Com um sinal de passa/falha **apertado** (que fica vermelho *neste* bug), você acha a causa. Sem ele, ficar lendo código não resolve. Gaste esforço desproporcional aqui.

Formas de montar, mais ou menos nesta ordem:
1. **Teste que falha** no ponto que alcança o bug (unitário, integração, e2e).
2. **Script `curl`/HTTP** contra o servidor de desenvolvimento.
3. **Comando de terminal** com uma entrada fixa, comparando a saída com uma saída boa conhecida.
4. **Navegador sem interface** (Playwright) que usa a página e confere DOM, console ou rede — o mais comum em site de cliente (botão de WhatsApp, formulário, layout em 375 px).
5. **Repetir uma requisição capturada**: salve o request/payload real e rode só aquele caminho.
6. **Harness descartável**: um pedaço mínimo do sistema com dependências falsas, chamando só a função suspeita.
7. **Loop de entradas aleatórias**: se é "às vezes dá errado", rode 1000 entradas e procure o padrão.
8. **Bisect**: se o bug apareceu entre dois estados (commit, versão), automatize "subir no estado X, checar" e use `git bisect run`.
9. **Comparar versões**: mesma entrada na versão antiga e na nova, e diff das saídas.
10. **Humano no ciclo** (último recurso): se só o usuário consegue reproduzir (login, celular dele), escreva um roteiro numerado de passos curtos e peça para ele responder cada observação ("o botão abriu o WhatsApp? s/n", "cole o erro do console"). Login fica com ele.

**Aperte o ciclo:** dá para ficar mais rápido (menos setup, escopo menor)? O sinal pode ser mais preciso (conferir o sintoma exato, não "não quebrou")? Mais determinístico (fixar data/hora, semente de aleatório, isolar rede)? Um ciclo de 30 s instável quase não ajuda; um de 2 s estável é superpoder.

**Bug intermitente:** o objetivo é aumentar a taxa de reprodução (repetir 100×, paralelizar, estressar). Bug que aparece 50% das vezes dá para depurar; 1%, não.

**Se não der para montar o ciclo:** pare e diga, listando o que tentou. Peça acesso ao ambiente que reproduz, um artefato capturado e censurado (HAR, log, gravação de tela com horário) ou permissão para instrumentação temporária. **Não siga para hipóteses sem ciclo.**

**Fase 1 termina** quando existe **um comando** que você já rodou pelo menos uma vez (mostre o comando e a saída, censurada) e que é:
- [ ] capaz de ficar vermelho: passa pelo caminho real do bug e confere o **sintoma exato que o usuário relatou**;
- [ ] determinístico;
- [ ] rápido (segundos);
- [ ] executável por você sem ajuda (humano só pelo roteiro do item 10).

Se você se pegar lendo código para montar teoria antes desse comando existir, **pare**: pular direto para a hipótese é exatamente o erro que esta skill evita.

## Fase 2: reproduzir e minimizar
Rode o ciclo e veja ficar vermelho. Confirme que é a falha que o **usuário** descreveu (bug errado = correção errada), que se repete, e guarde o sintoma exato.

Depois **minimize**: corte entradas, chamadas, configuração e passos **um de cada vez**, rodando o ciclo depois de cada corte, até sobrar só o que é necessário para falhar. Termina quando remover qualquer elemento deixa o ciclo verde.

## Fase 3: hipóteses
Gere **3 a 5 hipóteses ordenadas** antes de testar qualquer uma (uma só ancora na primeira ideia). Cada uma precisa prever algo:

> "Se a causa é X, então mudar Y faz o bug sumir / mudar Z piora."

Sem previsão, é palpite: descarte ou afine. **Mostre a lista ao usuário antes de testar** — ele pode saber que "subi uma mudança na #3 ontem". Se ele não estiver presente, siga sua ordem.

## Fase 4: instrumentar
Cada sonda testa uma previsão da Fase 3. **Mude uma variável por vez.** Prefira debugger/REPL; depois, logs pontuais nas fronteiras que separam as hipóteses; nunca "logar tudo e procurar".

**Rastreie para trás, não conserte onde estoura.** O erro costuma aparecer longe da causa (arquivo salvo na pasta errada, valor `undefined` três chamadas depois). Do ponto onde estourou, pergunte "quem chamou isso, com que valor?" e suba a cadeia até achar **onde o dado errado nasceu**. Corrija lá. Corrigir no sintoma deixa a origem viva para quebrar outro lugar.

**Marque todo log de debug** com um prefixo único, ex.: `[DEBUG-a4f2]`, para a limpeza virar um `grep`.

**Lentidão:** log costuma enganar. Meça uma linha de base (cronômetro, `performance.now()`, Lighthouse, profiler, plano de query) e depois bisecte. Medir primeiro, corrigir depois.

## Fase 5: correção + teste de regressão
Escreva o teste de regressão **antes** da correção, mas só se houver um ponto de teste que exercite o padrão real do bug. Se o único ponto disponível é raso demais para pegar o bug, um teste ali dá falsa segurança: anote isso como achado (a arquitetura está impedindo travar o bug).

Com um bom ponto: transforme a reprodução mínima num teste que falha → veja falhar → corrija → veja passar → rode de novo o ciclo da Fase 1 no cenário original.

Mudança cirúrgica: corrija só a causa, sem refatorar o resto (regras da `site-builder`).

Prove que o teste pega o bug: com a correção passa → **desfaça a correção → tem que falhar** → refaça → passa.

**Bug que veio de dado inválido:** além de corrigir a origem, valide onde o dado entra (formulário, API, parâmetro de URL). Uma validação só na entrada é o mínimo; em dinheiro, login ou dado de cliente, valide também onde o dado é usado. O objetivo é deixar o bug impossível, não só corrigido.

**Regra das 3 tentativas:** se 3 correções seguidas não resolveram, **pare de corrigir**. Três falhas indicam que a hipótese de base ou a arquitetura está errada, não que falta "só mais um ajuste". Volte à Fase 3 com o que as tentativas ensinaram e mostre ao usuário antes da quarta.

## Fase 6: limpeza (obrigatória)
- [ ] A reprodução original não reproduz mais.
- [ ] O teste de regressão passa (ou a falta de ponto de teste está documentada).
- [ ] Todos os logs `[DEBUG-...]` removidos (`grep` pelo prefixo).
- [ ] Protótipos descartáveis apagados ou numa pasta claramente marcada.
- [ ] A hipótese que se confirmou está escrita no commit/PR, para o próximo aprender.

Se o bug veio do relatório da `site-tester` (se você tiver essa skill), atualize o registro `BUG-xx` com a causa e a correção.