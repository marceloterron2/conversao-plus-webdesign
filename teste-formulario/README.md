# Conversão Plus — Variante B do teste A/B com HubSpot

A landing page nesta pasta foi duplicada da original para testar a captura de leads por formulário. A versão original na raiz do repositório continua intacta.

## Funcionamento
- Os cinco CTAs comerciais apontam para #formulario na mesma página com rolagem suave.
- O botão flutuante vermelho leva ao formulário.
- EXCEÇÃO: o botão do pop-up de saída permanece no WhatsApp pelo link CQC https://api.cqc.onpromedia.com.br/t/1A422BE8 .
- Campos: nome completo, possui site (Sim/Não), Instagram (opcional), e-mail, WhatsApp e consentimento.
- Apenas após confirmação de recebimento pelo HubSpot, o visitante acessa ./obrigado.html.
- Falhas de validação ou envio mantêm o formulário preenchido e mostram erro.

## Integração HubSpot: o que falta configurar
O site ainda não recebe leads reais no HubSpot. O ID da conta (portalId = 51184680) já foi preenchido e as propriedades foram mapeadas. Falta somente o formGuid de um formulário HubSpot próprio. Enquanto o código tiver esse placeholder, não envia nem redireciona, para evitar perder contatos.

1. Em HubSpot → Marketing → Formulários, crie um formulário chamado: Conversão Plus — Solicitação de Site Profissional (Teste B).
2. Adicione e publique os campos vinculados às propriedades de contato:
   - firstname — nome (propriedade padrão)
   - lastname — sobrenome (propriedade padrão)
   - email — e-mail (padrão)
   - phone — telefone (padrão)
   - voc_j_tem_um_site_hoje — propriedade existente de texto: Sim ou Não
   - instagram_empresa — propriedade existente de texto
3. Configure no HubSpot o consentimento para processamento dos dados em alinhamento com a finalidade informada no formulário. Não inscreva automaticamente o contato em comunicações de marketing.
4. Publique o novo formulário. Ele aparecerá na lista de formulários conectados ao HubSpot. Se preferir, copie o formId (GUID) pelo código de incorporação.
5. Edite somente a constante do GUID no arquivo teste-formulario/index.html:
   HUBSPOT_PORTAL_ID = '51184680'; // já configurado
   HUBSPOT_FORM_ID = 'SEU_FORM_GUID'; // trocar pelo GUID do novo formulário
6. O mapeamento de propriedades reais da conta foi confirmado pela conexão: firstname, lastname, email, phone, voc_j_tem_um_site_hoje e instagram_empresa. Os nomes no novo formulário devem corresponder exatamente.
7. Não coloque tokens privados, senhas ou chaves secretas no HTML. Esta integração usa o endpoint público do HubSpot.
8. Faça um envio de teste e confira os registros em Marketing → Formulários e CRM → Contatos antes de direcionar anúncios.

## Rastreio e análise
- Formulário utiliza o endpoint público https://api.hsforms.com/submissions/v3/integration/submit/{portalId}/{formGuid}
- O URL completo da página é enviado como pageUri, incluindo parâmetros de campanha. Valores de utm_* e gclid também estão em campos ocultos na página, mas não são enviados como propriedades extras sem a criação das propriedades no HubSpot.
- Se o tracking HubSpot estiver ativo, o cookie hubspotutk é incluído no envio, vinculando a navegação anterior ao contato. Instale o script de rastreamento do HubSpot caso deseje essa associação.
- Depois de envio confirmado, obrigado.html emite lead_formulario_enviado no dataLayer somente uma vez.
- Configure uma conversão de formulário própria no Google Tag Manager/Google Ads, diferente da conversão de clique do WhatsApp.
- O pop-up de saída usa o rastreador CQC separado da campanha de formulário.
- IDs existentes: GTM-MMH3K29P e Google Ads AW-18520976220.
- Controle acesso dos contatos no CRM, atualize a política de privacidade e respeite as regras de tratamento de dados.
- O endpoint v3 é legado e, conforme anúncio do HubSpot, ficará sem suporte a partir de setembro de 2027; acompanhe futuras orientações de migração.

## URLs esperadas (com GitHub Pages ativo)
- Original: /conversao-plus-webdesign/
- Variante B: /conversao-plus-webdesign/teste-formulario/
- Obrigado: /conversao-plus-webdesign/teste-formulario/obrigado.html
