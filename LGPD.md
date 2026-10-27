# Work Hub — adequação à LGPD (Lei 13.709/2018)

## O que foi corrigido no código (`Work_hub.html`)

| Problema | Correção | Base legal |
|---|---|---|
| Nenhum aviso sobre o envio de documentos ao Google Gemini | Aviso de privacidade obrigatório antes da 1ª chamada à IA, com registro do aceite (versão + data). Sem aceite, nada é enviado. Acesso permanente pelo ícone de escudo no Hub. | art. 6º VI, art. 9º |
| Dados pessoais enviados sem filtro à IA | Pseudonimização automática antes do envio: e-mail, CPF, RG, telefone, CEP e nomes após rótulos ("Responsável:", "Elaborado por:"…) viram `{{DPn}}`. A resposta é restaurada localmente, então o documento final não muda. Ligado por padrão. | art. 6º III, art. 13 |
| Chave de API na URL (`?key=`), que fica gravada em logs de proxy e no histórico | A chave agora vai no cabeçalho `x-goog-api-key` | art. 46 |
| Fotos enviadas com metadados EXIF (GPS, aparelho, autor) | A imagem é redesenhada num canvas antes do envio, o que descarta todos os metadados | art. 6º III |
| Ditado por voz enviava o áudio ao Google/Microsoft sem aviso | Confirmação de privacidade antes do 1º uso do microfone | art. 9º |
| Sem forma de exercer o direito de eliminação | Botão "Apagar todos os meus dados deste navegador" na janela de Backup | art. 18 VI |
| Texto da chave dizia que ela "não sai daqui" | Texto corrigido e aviso sobre a camada gratuita do Gemini | art. 6º VI |
| Backup sem alerta de conteúdo | Aviso de que o arquivo contém os dados salvos e deve ser guardado com segurança | art. 46 |

## Pendências da empresa (não se resolvem no código)

1. **Chave de API da camada paga.** Na camada gratuita do Gemini API, o Google pode usar o conteúdo enviado para melhorar os produtos dele, e revisores humanos podem lê-lo. Use uma chave de um projeto com faturamento ativado, aprovado pela TI.
2. **Contato do Encarregado (DPO).** Preencha a constante `LGPD_CONTATO_ENCARREGADO` no código com o canal oficial (art. 41).
3. **Transferência internacional (art. 33).** O jurídico ou o DPO deve validar a base para o envio de dados ao Google (cláusulas contratuais do Google Cloud ou Workspace).
4. **Registro da operação de tratamento (art. 37).** Incluir o Work Hub no inventário de dados da empresa.
5. **Fontes e bibliotecas externas.** Google Fonts, jsDelivr e o Tailwind CDN recebem o IP de quem abre a página. Para eliminar isso, hospede esses arquivos no servidor interno.

## Limites do mascaramento automático

O mascaramento reconhece padrões. Nomes soltos no texto, sem um rótulo antes, e o conteúdo de imagens (rostos, crachás, assinaturas) não são detectados. O aviso de privacidade orienta o usuário a revisar o material antes de enviar.

Se o texto do aviso mudar, aumente `LGPD_VERSAO_AVISO` para que todos aceitem de novo.
