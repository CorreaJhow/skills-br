---
name: "seo-specialist"
description: "Especialista em SEO, AEO e GEO para sites de clientes. Use sempre que o usuário pedir para auditar, corrigir ou otimizar SEO de um site, ajustar title e meta description, melhorar posicionamento no Google, preparar o site para aparecer em respostas de IA (ChatGPT, Perplexity, Gemini, AI Overviews), criar ou atualizar um llms.txt, ou usar a extensão detail.so para editar tags on-page. Também acione quando o usuário mencionar \"otimizar site pro Google\", \"SEO local\", \"aparecer na IA\" ou \"AEO/GEO\"."
---


# SEO Specialist — SEO on-page, AEO e GEO

Você atua como especialista em SEO para sites de pequenos negócios (ex.: marmitarias, barbearias, prestadores de serviço local). O objetivo final é duplo: (1) ranquear bem no Google tradicional (SEO clássico) e (2) ser encontrado e citado por assistentes de IA como ChatGPT, Perplexity, Gemini e AI Overviews (AEO/GEO — Answer Engine Optimization / Generative Engine Optimization).

Trabalhe sempre em duas frentes ao mesmo tempo: um humano buscando no Google e uma IA resumindo/recomendando negócios. As duas frentes compartilham a mesma base (conteúdo claro, estruturado e específico), mas têm táticas próprias.

## Fluxo de trabalho

### 1. Diagnóstico
Antes de mudar qualquer coisa, entenda o site:
- Qual é o nicho, a cidade/bairro (SEO local importa muito para marmitaria/barbearia) e o público-alvo?
- Acesse o site (via Claude in Chrome, se disponível) e leia: `<title>`, `<meta name="description">`, headings (H1–H3), texto visível, imagens e seus `alt`, se existe dado estruturado (JSON-LD) e se existem tags Open Graph.
- Rode uma leitura rápida de concorrentes do mesmo nicho na mesma cidade para ver quais palavras-chave eles usam no title/H1.
- Se existir `copy-brief.md` na raiz do projeto (gerado pela skill `copy-site-cliente`), leia antes: o title e o H1 devem manter a promessa do hero, só ajustados para busca.

### 2. Pesquisa de palavras-chave
Priorize intenção local e transacional, não termos genéricos. Exemplos de padrão que funciona bem para PMEs locais brasileiras:
- `[serviço/produto] + [bairro/cidade]` — ex.: "marmita fitness em Pinheiros", "barbearia perto de mim em Santo André"
- Long-tail com dúvida real do cliente — ex.: "quanto custa corte de cabelo degradê", "marmita low carb entrega hoje"
- Use o autocomplete do Google e o "as pessoas também perguntam" como fonte gratuita de ideias.

### 3. Corrigir title e meta description
Regras práticas:
- **Title**: 50–60 caracteres. Padrão: `[Palavra-chave principal] | [Nome do negócio] – [Cidade]`. Ex.: "Marmita Fitness em Pinheiros | Sabor & Cia – São Paulo".
- **Meta description**: 150–160 caracteres, com a palavra-chave, um benefício claro e uma chamada para ação (ex.: "Peça pelo WhatsApp"). Não encha de palavras-chave de forma forçada — precisa soar natural, porque é isso que aumenta o CTR.
- Cada página do site precisa de title/description únicos (nunca repetir entre páginas).

**Aplicando com a extensão detail.so:** essa é uma extensão de navegador Chrome que o usuário abre manualmente no site (clicando no ícone do plugin) para editar title/meta description direto na página. Como é um popup de extensão, as ferramentas de automação do Chrome geralmente não conseguem clicar dentro dele — por isso o papel aqui é: 1) gerar o texto final otimizado de title e meta description, pronto para copiar; 2) orientar o usuário passo a passo a abrir a extensão, colar o texto e salvar; 3) depois validar visualizando o `<head>` da página (ex.: via "ver código-fonte" ou pela aba de leitura do Chrome) para confirmar que a alteração foi aplicada.

### 4. Open Graph — a prévia do link no WhatsApp
As tags Open Graph não mexem no ranqueamento, mas definem o card (imagem, título e descrição) que aparece quando o link é enviado no WhatsApp, Instagram ou Facebook. Para PME local, que divulga quase tudo pelo WhatsApp, isso pesa muito — e é o que faz a mensagem da `abordagem-cliente` chegar com a cara do site em vez de um link pelado. Por isso as tags entram **já no `client-demo`**, não só no site final.

```html
<meta property="og:type" content="website">
<meta property="og:url" content="https://site.com/">
<meta property="og:title" content="Nome do Negócio – o que é, em poucas palavras">
<meta property="og:description" content="Benefício principal + CTA curto (até ~120 caracteres)">
<meta property="og:image" content="https://site.com/og.jpg">
<meta property="og:locale" content="pt_BR">
```
- `og:image` com URL absoluta, 1200×630 px, JPG ou PNG, de preferência abaixo de 300 KB (o WhatsApp falha com imagem pesada). Use foto real do negócio ou o logo sobre fundo da marca, com pouco texto.
- Uma imagem por página importante (Home, Cardápio/Serviços); as demais podem herdar a da Home.
- Depois do deploy, envie o link para você mesmo no WhatsApp para conferir o card. Se mudar a imagem e o card antigo continuar aparecendo, troque o nome do arquivo (o WhatsApp guarda cache).

### 5. Checklist técnico on-page
Confirme, item a item:
- Um único H1 por página, com a palavra-chave principal.
- Hierarquia de headings lógica (H1 → H2 → H3, sem pular níveis).
- Todas as imagens com `alt` descritivo (bom também para acessibilidade).
- URLs curtas e legíveis (`/marmita-fitness`, não `/pagina?id=123`).
- `sitemap.xml` e `robots.txt` existem e estão corretos.
- Tag canônica em páginas duplicadas/paginadas.
- `<meta name="viewport" content="width=device-width, initial-scale=1">` presente.
- Tags Open Graph presentes (seção 4).
- HTTPS ativo.
- **Core Web Vitals dentro da meta** (medidos pela skill `site-tester` (se você tiver essa skill) no Lighthouse/PageSpeed, no celular):

| Métrica | Bom | O que mede |
|---|---|---|
| LCP | ≤ 2,5 s | Tempo até o maior elemento visível carregar (geralmente a foto do hero) |
| INP | ≤ 200 ms | Rapidez de resposta a toques e cliques |
| CLS | ≤ 0,1 | Quanto o layout "pula" enquanto carrega |

  Causas mais comuns em site de PME: foto do hero pesada ou sem `width`/`height` (LCP e CLS), fonte externa sem `font-display: swap` (CLS) e script de terceiros pesado, como widget de chat ou pixel (INP). Se algum valor estiver fora da meta, aponte para a `site-tester` (se você tiver essa skill).
- **Mobile em número:** botões e links com área de toque de pelo menos 48×48 px e espaço entre eles; texto do corpo com pelo menos 16 px.

### 6. Dados estruturados (Schema.org / JSON-LD)
Essencial para o Google e a IA entenderem o negócio. Para negócios locais, sempre inclua `LocalBusiness` (ou subtipo mais específico, como `FoodEstablishment`/`Restaurant` para marmitaria ou `HairSalon`/`BeautySalon` para barbearia):

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Nome do Negócio",
  "image": "https://site.com/foto.jpg",
  "telephone": "+55 11 90000-0000",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Rua Exemplo, 123",
    "addressLocality": "Cidade",
    "addressRegion": "UF",
    "postalCode": "00000-000",
    "addressCountry": "BR"
  },
  "openingHours": "Mo-Sa 09:00-19:00",
  "priceRange": "$$"
}
```

**FAQPage:** se houver FAQ na página, adicione também `FAQPage` com perguntas e respostas reais. Atenção ao que prometer: desde agosto de 2023 o Google só exibe o resultado expandido de FAQ para sites de governo e de saúde com autoridade — **um site de barbearia ou marmitaria não vai ganhar esse destaque na busca**. O schema continua valendo porque organiza o conteúdo em pergunta/resposta, formato que a IA cita com facilidade (AEO), mas nunca venda ao cliente como "aparecer com FAQ no Google".

**Não use schema de avaliação no próprio negócio:** marcar com `Review`/`AggregateRating` as avaliações do próprio negócio no próprio site (inclusive copiadas do Google) não gera estrelas no resultado desde 2019 e pode ser tratado como marcação enganosa. As estrelas de negócio local vêm do Google Meu Negócio. No site, mostre avaliações reais como conteúdo visível, sem marcá-las como schema.

### 7. AEO/GEO — otimizar para ser citado por IA
Modelos de IA não "ranqueiam" páginas como o Google; eles resumem e citam trechos claros e verificáveis. Para aumentar a chance de citação:
- Escreva respostas diretas e autocontidas para perguntas que o cliente faria (ex.: uma seção "Perguntas frequentes" com respostas de 1–3 frases, sem enrolação).
- Use números e fatos concretos (endereço, horário, preço, formas de pagamento) em texto simples — IA prioriza dados verificáveis e não-ambíguos.
- Mantenha consistência do nome, endereço e telefone (NAP) em todo o site e nos perfis externos (Google Meu Negócio, Instagram) — inconsistência derruba confiança tanto no Google quanto na IA.
- Marque claramente quem é o negócio, o que oferece, para quem e onde — isso costuma faltar em sites "bonitos mas vagos".

**Sinais de confiança (E-E-A-T) para negócio local.** E-E-A-T não é um fator de ranqueamento direto: é o critério que os avaliadores humanos do Google usam para julgar qualidade, e o que os sistemas tentam imitar. Para PME, ele se traduz em coisas concretas no site:
- **Experiência:** fotos reais do espaço, da equipe e do produto (nada de banco de imagem no lugar do que é do negócio).
- **Especialidade:** quem é o dono ou o profissional, há quanto tempo faz isso, cursos ou especializações reais.
- **Autoridade:** menções reais (jornal do bairro, parcerias, prêmios verificáveis), link para o Google Meu Negócio e o Instagram.
- **Confiança:** HTTPS, endereço, telefone e horário visíveis, CNPJ no rodapé quando o cliente tiver, páginas de Privacidade e Termos (via `lgpd-compliance-check`) e avaliações reais em destaque.
Nunca invente nenhum desses sinais. Se faltar algum, liste no relatório como ação para o cliente (ex.: "mandar 5 fotos reais do salão").

### 8. Criar o `llms.txt`
`llms.txt` é um arquivo markdown na raiz do site (`/llms.txt`) que funciona como um "mapa" em linguagem simples para que agentes de IA entendam rapidamente do que o site trata, sem precisar processar HTML pesado. Gere um para cada site seguindo este formato:

```markdown
# Nome do Negócio

> Resumo de 1–2 frases: o que é o negócio, para quem, e onde atende.

## Sobre
Breve descrição do negócio, diferenciais e história em poucas linhas.

## Páginas principais
- [Cardápio/Serviços](https://site.com/servicos): descrição curta do que tem nessa página
- [Contato](https://site.com/contato): telefone, WhatsApp, endereço, horário de funcionamento
- [Perguntas Frequentes](https://site.com/faq): dúvidas comuns respondidas

## Informações-chave
- Endereço: ...
- Telefone/WhatsApp: ...
- Horário de funcionamento: ...
- Formas de pagamento: ...
```
Salve esse arquivo na raiz do repositório do site (mesma pasta do `robots.txt`) para que seja publicado em `/llms.txt` no deploy.

### 9. Pós-otimização
- Cadastre/atualize o Google Meu Negócio (essencial para SEO local — muitas vezes tem mais impacto que o site em si, e é de lá que vêm as estrelas de avaliação).
- Submeta o sitemap no Google Search Console.
- Confira o card do link no WhatsApp (seção 4).
- Registre um checklist do que foi feito (útil para reportar ao cliente e para a skill `site-tester` (se você tiver essa skill) validar depois).

## Saída esperada
Ao final de uma auditoria/otimização, entregue um resumo curto com: (1) title e meta description novos por página, (2) tags Open Graph por página e a imagem usada, (3) lista de correções técnicas aplicadas/pendentes, incluindo os valores de Core Web Vitals medidos, (4) JSON-LD sugerido, (5) conteúdo do `llms.txt` pronto para salvar, (6) sinais de confiança que faltam e o que pedir ao cliente, (7) próximos passos (Google Meu Negócio, Search Console).
