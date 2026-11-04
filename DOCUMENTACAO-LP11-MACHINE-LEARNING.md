# Documentação — LP 11 | Machine Learning para Empresas

## 1. Objetivo
Landing page estática da ON Solutions Brasil que apresenta o serviço de Machine Learning para empresas e leva o visitante ao WhatsApp comercial (`5511972243329`) com uma mensagem pronta.

## 2. Escopo
Implementação fiel ao HTML de referência `11-lp-machine-learning-para-empresas.html`, sem seções, textos ou funcionalidades adicionais. O CSS e o JS originais, que estavam embutidos no HTML, foram separados em arquivos próprios.

## 3. Arquitetura
HTML5, CSS3 e JavaScript puro. Sem frameworks, backend, banco de dados ou bibliotecas. Única dependência externa: Google Fonts (Poppins 400–800) e, opcionalmente, GTM/GA4/Google Ads (só carregam se os IDs forem preenchidos).

## 4. Estrutura dos arquivos
```text
index.html
css/styles.css
js/main.js
assets/img/favicon.png          (a fornecer)
assets/img/on-logo.png          (a fornecer)
assets/img/clientes/*.png       (a fornecer)
DOCUMENTACAO-LP11-MACHINE-LEARNING.md
README.md
```

## 5. Seções implementadas (ordem da referência)
Header, Hero, "Você se reconhece?" (4 desafios), "O que você ganha" (4 benefícios), "Quem confia na ON" (indicadores + carrossel), "Como funciona" (3 passos), "Conversa gratuita", "Dúvidas" (3 perguntas), CTA final, Footer e botão fixo de WhatsApp.

## 6. Recursos visuais
Paleta ON (`#0B1220`, `#0F172A`, `#F5F8FB`, `#E2E8F0`, `#52627A`, `#5EEAD4`, `#0D9488`, `#0F766E`, `#25D366`, `#1EBE5B`), fonte Poppins, ícones SVG inline, gradientes verde/azul-petróleo no hero e na seção de conversa gratuita.

## 7. Funcionalidades
- Header sticky que esconde ao rolar para baixo, reaparece ao rolar para cima, fica visível perto do topo (< 80px) e ao receber foco.
- Seleção múltipla de desafios com `aria-pressed`.
- Mensagem do WhatsApp dinâmica e sincronizada.
- Carrossel infinito de clientes (pausa no toque, desativado com `prefers-reduced-motion`).
- FAQ com `<details>/<summary>` (teclado nativo).
- Rastreamento de cliques.

## 8. Seleção de desafios
Cada botão `.pain` alterna `aria-pressed`. O texto de `data-q` é usado sem a pontuação final.
- 0 selecionados: mensagem-base, sem feedback.
- 1: `... Meu maior desafio hoje: [opção].` + "Pronto! Agora toque em “Pedir orçamento no WhatsApp” para enviar."
- 2+: `... Meus maiores desafios hoje: [a]; [b].` + "Você marcou [N]. Isso tem solução: toque em “Pedir orçamento no WhatsApp” para enviar."

## 9. Mensagem do WhatsApp
Base: `Olá, vim do site e gostaria de saber mais sobre os serviços de Machine Learning.` Links `https://wa.me/5511972243329?text=` + `encodeURIComponent(...)`, `target="_blank"`, `rel="noopener"`. Os elementos com `data-wa-main` (topo-telefone, topo, barra-fixa) são atualizados a cada seleção. Com `ON_APPEND_ORIGIN = true`, parâmetros `utm_term`/`kw`, `utm_campaign` e `gclid` acrescentam `Origem: anúncio | Termo: … | Campanha: …`.

## 10. Card de prévia
O balão `[data-bubble]` do hero recebe o mesmo texto da mensagem (sem o sufixo de origem).

## 11. Rastreamento
`ON_TRACKING = { gtmId: "", ga4Id: "", gadsId: "", gadsConversionLabel: "" }`, todos vazios (nenhum ID inventado). Em cada clique em link `wa.me` é disparado um único evento `whatsapp_click` no `dataLayer` (`service: "Machine Learning"`, `position`) e, se o `gtag` existir, `generate_lead` (e a conversão do Ads, se houver label). Posições: `topo-telefone`, `topo`, `barra-fixa`.

## 12. SEO
Title, description, canonical (`https://onsolutionsbrasil.com.br/lp/machine-learning-para-empresas/`), robots `noindex,follow` e theme-color `#0B1220`, iguais à referência.

## 13. Responsividade
Mobile-first, com ajustes em 430px, 400px, 380px, 340px e 860px. Cards de benefícios em 4 colunas no desktop; hero em 2 colunas; botão fixo respeita `env(safe-area-inset-bottom)`; sem menu hambúrguer.

## 14. Acessibilidade
HTML semântico, hierarquia h1/h2/h3, `:focus-visible`, `aria-pressed`, `aria-live="polite"` no feedback, `aria-hidden` nos ícones e nos clones do carrossel, `prefers-reduced-motion`.

## 15. Testes realizados
- `node --check js/main.js`: sem erros de sintaxe.
- Conferência do conteúdo textual do HTML contra a especificação.
- **Não realizados**: teste em navegador, comparação visual lado a lado com a referência e teste nas resoluções 340/380/400/430/860px. O ambiente não tinha o arquivo de referência nem navegador disponível.

## 16. Pendências
1. **Imagens**: o arquivo de referência não estava em disco, e os logotipos estavam em base64 dentro dele. É preciso salvar `favicon.png`, `on-logo.png` e os logos em `assets/img/clientes/` (`braziliana`, `quatri-automacao`, `brooks-construtora`, `crosshr`, `multilife-care`, `mafedo-engenharia`, todos `.png`). Enquanto faltarem, os logos de clientes caem para o nome em texto (fallback adicionado em `main.js`, não existente na referência).
2. **Links do footer** (LGPD e Política de privacidade) permanecem `href="#"`, como na referência, até haver URLs reais.
3. **CTA final**: como na referência, não tem botão próprio; orienta o uso do botão fixo.
4. **IDs de rastreamento** a preencher.
