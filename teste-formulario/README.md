# Conversão Plus — Variante B com formulário oficial HubSpot

Este diretório contém a landing page de teste de formulário. O site original na raiz do repositório permanece inalterado.

## Integração ativa no código

O formulário manual foi substituído pelo código oficial fornecido pelo proprietário da conta:

```html
<script src="https://js.hsforms.net/forms/embed/51184680.js" defer></script>
<div class="hs-form-frame" data-region="na1" data-form-id="f8aadaca-da2f-46c6-8aa6-00486f0ff45f" data-portal-id="51184680"></div>
```

Os dados e os campos são geridos pelo formulário publicado no HubSpot, de ID `f8aadaca-da2f-46c6-8aa6-00486f0ff45f`. A configuração dos campos obrigatórios, consentimento e notificações deve ser feita diretamente no HubSpot. Não existe mais o formulário manual nem o código legado de envio API no HTML.

## Comportamento
- Os 5 CTAs principais mostram **Solicitar orçamento**, sem setas, e apontam para `#formulario` na mesma página.
- O título e subtítulo redundantes do card do formulário foram removidos.
- O pop-up de saída e o botão flutuante antigos foram removidos; o **novo widget de chat CQC** fornecido pelo proprietário mostra um botão flutuante verde, abre um chat e usa o endereço `https://api.cqc.onpromedia.com.br/t/720FD7D8` ao clicar em **Iniciar conversa**.
- Um ouvinte do evento global `hs-form-event:on-submission:success` verifica o ID do formulário, emite `lead_formulario_enviado` no `dataLayer` da landing page e redireciona para `https://sites.conversaoplus.com.br/obrigado/`. Erros de envio não redirecionam.
- O antigo arquivo `teste-formulario/obrigado.html` permanece no repositório por histórico, mas **não faz parte do fluxo atual**.

## Configuração de rastreamento
- GTM `GTM-MMH3K29P`
- Google Ads `AW-18520976220`
- O evento `lead_formulario_enviado` deve ser configurado como conversão em GTM/Google Ads.
- **Não use o ID de conversão do clique no WhatsApp para o envio do formulário**.
- A página de obrigado fica em outro domínio/subdomínio. A chave `sessionStorage` do site de formulário **não é compartilhada entre origens**. Por isso o evento de lead é registrado na landing page depois do sucesso, não deve depender do marcador de sessionStorage da página de obrigado externa.
- Se for medir apenas visitantes que chegaram à página externa, configure no GTM um evento específico e teste a atribuição entre domínios. Não dispare um segundo evento de lead na mesma jornada sem deduplicação.

## Validação antes da campanha
1. Abra a variante em `https://marceloterron2.github.io/conversao-plus-webdesign/teste-formulario/` (se o GitHub Pages estiver habilitado).
2. Confira que o formulário do HubSpot carrega com todos os campos necessários.
3. Preencha um registro de teste, envie e confira que a entrada aparece no HubSpot.
4. Confirme a navegação para `https://sites.conversaoplus.com.br/obrigado/`.
5. Valide o evento no Tag Assistant / modo de visualização do GTM.
6. Revise a configuração "Ao enviar" do formulário no HubSpot. Se também usar um redirecionamento nativo, utilize a mesma URL de obrigado para evitar destinos conflitantes.

Documentação: https://developers.hubspot.com/docs/api-reference/latest/marketing/forms/global-form-events
