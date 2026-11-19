---
name: verificar-antes-de-concluir
description: Use antes de dizer que algo está pronto, corrigido, passando ou entregue (site de cliente, código, deploy, tarefa de subagente), antes de commit, PR, deploy ou de mandar algo pro cliente — rodar a verificação e ler a saída antes de afirmar.
---

# Verificar antes de concluir

Adaptado de `verification-before-completion` do Superpowers (obra/superpowers, MIT, © 2025 Jesse Vincent).

**Regra:** nenhuma afirmação de "pronto" sem prova rodada **nesta mensagem**. Se não rodou agora, não pode dizer que passa.

## O portão
Antes de qualquer "pronto", "corrigido", "passou", "no ar":
1. **Qual comando prova isso?** (teste, build, Lighthouse, curl, abrir a página)
2. **Rode inteiro**, do zero, não reaproveite saída antiga.
3. **Leia a saída**: código de saída, quantos falharam, avisos.
4. **A saída confirma?** Não → diga o estado real com a prova. Sim → afirme **junto com a prova**.

## O que prova o quê
| Afirmação | Prova | Não basta |
|---|---|---|
| Testes passam | saída do teste com 0 falhas | "deve passar", rodada antiga |
| Build ok | `npm run build` com saída 0 | lint passou |
| Bug corrigido | o sintoma original testado e sumiu | "mudei o código" |
| Teste de regressão vale | passa → desfaz correção → falha → refaz → passa | passou uma vez |
| Site no ar | URL de produção aberta, 200, conteúdo certo, celular 375 px | deploy da Vercel "Ready" |
| Formulário/WhatsApp funciona | envio real de teste, mensagem chegou / link abre com o texto certo | botão aparece |
| Subagente terminou | `git diff` mostra a mudança e você conferiu | o subagente disse "sucesso" |
| Pedido do cliente atendido | proposta/escopo relido item por item | "os testes passam" |

## Sinais de alerta (pare e verifique)
- Palavras como "deve", "provavelmente", "parece que".
- Comemorar antes de rodar ("Perfeito!", "Pronto!").
- Ir fazer commit, push, deploy ou mandar link pro cliente sem ter rodado nada.
- Confiar no relatório de um subagente ou ferramenta sem olhar o resultado.

## Em site de cliente
Antes de mandar qualquer link pro cliente ou dizer que está no ar: rode a parte relevante da `site-tester` (se você tiver essa skill; senão, pelo menos build + abrir em 375 px e 1440 px + CTA/WhatsApp + formulário) e mostre o que viu. Prova curta no relatório: o comando e a linha que importa da saída.
