---
title: "Editor do Gerenciador de Conex&#245;es SMTP | Microsoft Docs"
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
  - "sql13.dts.designer.smtpconnection.f1"
helpviewer_keywords: 
  - "Editor do Gerenciador de Conexões SMTP"
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# Editor do Gerenciador de Conex&#245;es SMTP
  Use a caixa de diálogo **Editor do Gerenciador de Conexões SMTP** para especificar um servidor SMTP.  
  
 Para saber mais sobre o Gerenciador de Conexões SMTP, consulte [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md).  
  
## Opções  
 **Nome**  
 Forneça um nome exclusivo para o gerenciador de conexões.  
  
 **Description**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Servidor SMTP**  
 Forneça o nome do servidor SMTP.  
  
 **Usar Autenticação do Windows**  
 Selecione para enviar email usando um servidor SMTP que usa a Autenticação do Windows para autenticar o acesso ao servidor.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões SMTP dá suporte apenas para autenticação anônima e Autenticação do Windows. Ele não suporta a autenticação básica.  
  
> [!NOTE]  
>  Ao utilizar o Microsoft Exchange como servidor SMTP, talvez seja preciso definir **Usar Autenticação do Windows** como **True**. Os servidores do Exchange podem ser configurados para não permitir conexões SMTP não autenticadas.  
  
 **Habilitar SSL (Secure Sockets Layer)**  
 Selecione para criptografar a comunicação utilizando a SSL (Secure Sockets Layer) ao enviar mensagens de email.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  