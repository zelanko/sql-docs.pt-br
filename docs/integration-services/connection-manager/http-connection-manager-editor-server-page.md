---
title: "Editor do Gerenciador de Conex&#245;es HTTP (p&#225;gina Servidor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.httpconnection.server.f1"
helpviewer_keywords: 
  - "Editor do Gerenciador de Conexões de HTTP"
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# Editor do Gerenciador de Conex&#245;es HTTP (p&#225;gina Servidor)
  Use a guia **Servidor** da caixa de diálogo **Editor do Gerenciador de Conexões de HTTP** para configurar o Gerenciador de Conexões de HTTP especificando propriedades como URL e credenciais de segurança. Uma conexão HTTP permite que um pacote acesse um servidor Web usando o HTTP para enviar ou receber arquivos. Depois de configurar o Gerenciador de Conexões de HTTP, você também pode testar a conexão.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 Para obter mais informações sobre o gerenciador de conexões de HTTP, consulte [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Para saber mais sobre um cenário de utilização geral para o Gerenciador de Conexões de HTTP, consulte [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
## Opções  
 **Servidor URL**  
 Digite o URL do servidor.  
  
 Para usar o botão **Baixar WSDL** na página **Geral** do **Editor da Tarefa Serviço da Web** para baixar um arquivo WSDL, digite a URL do arquivo WSDL. Essa URL termina com "?wsdl".  
  
 **Usar credenciais**  
 Especifique se você o Gerenciador de Conexões de HTTP deve usar as credenciais de segurança do usuário para autenticação.  
  
 **Nome de usuário**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Senha**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Domínio**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Usar certificado do cliente**  
 Especifique se o Gerenciador de Conexões de HTTP deve usar um certificado do cliente para autenticação.  
  
 **Certificado**  
 Selecione um certificado na lista usando a caixa de diálogo **Selecionar Certificado**. A caixa de texto exibe o nome associado a este certificado.  
  
 **Tempo limite (em segundos)**  
 Forneça um tempo limite para conexão com o servidor Web. O valor padrão desta propriedade é 30 segundos.  
  
 **Tamanho da parte (em KB)**  
 Forneça um tamanho da parte para gravar dados.  
  
 **Testar Conexão**  
 Depois de configurar o Gerenciador de Conexões de HTTP, confirme se a conexão é viável clicando em **Testar Conexão**.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexões HTTP &#40;Página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)  
  
  