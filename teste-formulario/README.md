# TESTE A/B — CONVERSÃO PLUS

Esta pasta duplica a landing page original com um formulário em vez de CTAs para WhatsApp.
O index.html do site original na raiz foi preservado.

## Fluxo
- Todos os CTAs comerciais apontam para #formulario, inclusive botão flutuante e popup de saída.
- Campos: nome completo, possui site (sim/não), Instagram opcional, email e WhatsApp.
- Ao receber uma resposta de sucesso do Formspree, redireciona para obrigado.html.
- Com erro, mantém os dados preenchidos e mostra aviso, sem agradecer falsamente.

## CONFIGURAÇÃO OBRIGATÓRIA ANTES DE ANUNCIAR
1. Crie uma conta e um formulário em https://formspree.io/ .
2. Copie o endpoint fornecido, como https://formspree.io/f/abcdefgh .
3. No teste-formulario/index.html, substitua SEU_ID_AQUI no FORM_ENDPOINT pelo ID real.
4. Faça um envio de teste e confirme o recebimento no painel Formspree.
5. A página obrigado.html deve abrir somente após recebimento confirmado.
6. Confirme a política de privacidade/consentimento e o acesso à caixa dos leads.

Sem o endpoint o formulário NÃO envia nem redireciona: é proposital para evitar perda de leads.

## Links e ativos
- Original: /
- Teste: /teste-formulario/
- Obrigado: /teste-formulario/obrigado.html
- Os três arquivos de imagem do portfólio também foram copiados para teste-formulario/assets/portfolio/ .

## Medição
- Parâmetros utm_source, utm_medium, utm_campaign, utm_content, utm_term, gclid e fbclid são enviados como campos ocultos.
- GTM existente: GTM-MMH3K29P.
- Google Ads: AW-18520976220.
- Após envio confirmado, obrigado.html envia o evento dataLayer lead_formulario_enviado UMA vez.
- Configure a conversão própria do formulário no GTM/Google Ads; não reutilize a conversão de clique no WhatsApp.
