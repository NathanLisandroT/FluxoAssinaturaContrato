# Fluxo de Assinatura de Documentos

Este projeto descreve o fluxo completo de assinatura de documentos, utilizando PlugSign para assinatura digital e AWS para armazenamento seguro. O sistema implementa um processo de controle e gestão de documentos, integrando assinatura, armazenamento e exibição no frontend.

## Visão Geral

![Diagrama do Fluxo](https://imgur.com/tN5AiGw.png)

1. **Usuário Inicia a Ação**: O processo começa quando o usuário clica no botão "Assinar" no sistema.
2. **Envio para PlugSign**: O sistema envia o documento para o PlugSign, onde um ID exclusivo é gerado.
3. **Salvar no Banco de Dados**: O ID gerado é salvo no banco de dados com o status "PENDENTE".
4. **Envio para Assinatura no PlugSign**: O documento é enviado para ser assinado no PlugSign.
5. **Retorno via Webhook**: Após a assinatura ser concluída, o PlugSign envia um Webhook para o sistema informando que o documento foi assinado.
6. **Recuperação do DocumentKey**: O sistema utiliza o `documentKey` para recuperar o documento assinado.
7. **Envio para AWS**: O documento assinado é enviado para a AWS para armazenamento seguro.
8. **Atualização do Status no Banco de Dados**: O status do documento é atualizado para "ASSINADO" no banco de dados.
9. **Exibição dos Documentos no Frontend**:
    - O sistema consulta os documentKeys assinados no banco de dados e monta uma tabela comparando com os documentos armazenados na AWS.
    - O frontend exibe os documentos na tabela com os seguintes campos:
        - **Tipo de Contrato**: Guia PS, Guia Intercâmbio, Contrato do Beneficiário.
        - **Código ou Carteira**: Código da guia ou carteira do beneficiário.

## Recuperação e Exibição dos Documentos

Após a assinatura e envio dos documentos para a AWS, o sistema lista todos os documentos na AWS e os compara com os documentKeys assinados no banco de dados. No frontend, uma tabela é montada com as seguintes informações:

- **Tipo de Contrato**: Exibe o tipo de contrato ou guia.
- **Código ou Carteira**: Mostra a carteira do beneficiário ou código da guia, conforme o tipo do contrato.
- **Link para o Documento**: A AWS retorna o link do documento armazenado, que é salvo no botão "Baixar" na tabela.

## Fluxo Visual

Aqui está um resumo do fluxo implementado:


1. **Usuário Clica em "Assinar"**
2. **Gerar ID Exclusivo no PlugSign**
3. **Salvar ID no Banco de Dados (Status: PENDENTE)**
4. **Envio para Assinatura**
5. **Assinatura Concluída**
6. **Retorno via Webhook para o Sistema**
7. **Recuperação do DocumentKey**
8. **Envio do Documento Assinado para AWS**
9. **Atualização do Banco de Dados para "ASSINADO"**

### Front-End:
![Fluxo do Front-end](https://imgur.com/GDjxnUZ.png)
10. **Listar Documentos na AWS**
11. **Comparar DocumentKeys no Banco de Dados**
12. **Montar Tabela no Frontend**
13. **Salvar Link da AWS no Botão "Baixar"**
