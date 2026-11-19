---
name: humanizador-pt-br
description: Use quando o usuário quiser tirar a "cara de IA" de um texto em português (post, legenda, e-mail, artigo, descrição) ou revisar um texto antes de publicar. Acha os padrões que denunciam ChatGPT, reescreve preservando a voz de quem escreveu e entrega um relatório do que mudou.
---

# Humanizador PT-BR

Tira de um texto o que faz o leitor pensar "isso é ChatGPT" ou "isso é conta de marca". O objetivo **não** é passar em detector (ninguém garante isso, e em texto curto a nota é ruído): é o texto soar como uma pessoa escreveu.

Adaptado do humanizer de sergebulaev/instagram-skills (MIT), reescrito para o português.

## Dois modos

- **Revisar** ("revisa esse texto"): só diagnostica. Entrega o relatório, sem reescrever.
- **Reescrever** (padrão, "tira a cara de IA disso"): aplica os passos abaixo e entrega o texto novo mais o relatório.

## Antes de mexer

1. Se o usuário tiver textos antigos dele, leia 1 ou 2 pra pegar a voz: cacoetes, gírias, contrações, comprimento de frase. Sem amostra, pergunte em uma linha como ele fala, ou mantenha neutro.
2. Descubra o canal (Instagram, LinkedIn, e-mail, artigo). Muda o tom, não os padrões.

## Passos

**1. Limpar por densidade (a unidade é o parágrafo, não a palavra).** Conte marcadores por parágrafo: 1 = normal, deixa; 2 = avisa no relatório; 3 ou mais = reescreve o parágrafo inteiro. Nunca troque por sinônimo da mesma lista.
- Vocabulário: alavancar, potencializar, impulsionar, otimizar, elevar, desbloquear, destravar, mergulhar (fundo), explorar, navegar (figurado), transformar, revolucionar, robusto, essencial, crucial, fundamental, significativo, estratégico, abrangente, insights, jornada, cenário, ecossistema, universo de, virada de chave, sem dúvida, certamente, basicamente, em última análise.
- Gramática: frase abrindo com gerúndio ("Pensando nisso, ...", "Buscando mais qualidade, ...") e nominalização ("a implementação de", "a otimização do"). Troque por quem fez + verbo.

**2. Remover sempre, basta aparecer uma vez:**
- Pontes de revelação: "O resultado?", "E o melhor:", "Spoiler:", "Plot twist:", "Vamos falar sobre...", "A verdade é que...", "Pare de X, comece a Y".
- Paralelismo negativo: "Não é sobre X, é sobre Y", "Não é só X, é Y".
- Frases mortas: "no mundo de hoje", "na era digital", "no cenário atual", "game changer", "próximo nível", "no fim do dia".
- Sinceridade anunciada: "papo reto:", "sendo sincero", "vou ser honesto", "real talk", "opinião impopular:" quando é popular.
- Fechamentos de isca: "o que vocês acham?", "comenta aí", "marca 3 amigos", "curte se concorda".

**3. Travessão (—):** no máximo cerca de 1 a cada 100 palavras. O excesso vira vírgula, dois-pontos, parênteses ou quebra de linha.

**4. Ritmo (só como guarda).** Não fabrique variação. Remova staccato encenado ("Simples. Rápido. Fácil."), linha de uma palavra pra drama ("Pronto.", "Exato.") e pergunta-e-resposta falsa ("Por quê? Porque..."). Tríade oca ("mais rápido, mais leve, melhor") sai; lista de três com itens concretos pode ficar. Emoji: 0 a 3, com intenção.

**5. Acrescentar só o concreto.** Um número com referência, um nome próprio, um detalhe em primeira pessoa. Se não estiver no material, **pergunte**. Nunca invente fato, número ou história.

**6. Guarda contra exagero.** Releia: criei staccato? Achatei a voz? Se sim, volte atrás. Texto já limpo recebe 2 ou 3 toques, não uma cota. Na dúvida se é a pessoa ou a IA, deixe como está.

## Sempre preservar

Cacoetes da pessoa, gírias e contrações ("tá", "pra", "cê"), humor, o jeito de abrir frase, emojis que ela usa de propósito.

## Relatório

`APROVADO` / `APROVADO COM AVISOS` / `REPROVADO`, com: o que foi removido (por categoria), parágrafos com 3+ marcadores, contagem de travessões e a reescrita proposta. Mostre o antes e o depois só dos trechos que mudaram.

## Regras

- Nunca publicar nada. Entrega o texto pra copiar.
- Não mudar o sentido nem o fato do texto original.
- Texto curto demais (menos de 2 frases): diga que não há o que analisar, em vez de inventar problema.
