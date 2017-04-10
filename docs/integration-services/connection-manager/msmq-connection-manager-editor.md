---
title: "Editor do Gerenciador de Conex&#245;es MSMQ | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.msmqconnectionmanager.f1"
helpviewer_keywords: 
  - "Editor do Gerenciador de Conexões MSMQ"
ms.assetid: ef842cb4-82da-4550-85fe-9bedbc1e77c7
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Editor do Gerenciador de Conex&#245;es MSMQ
  Use a caixa de diálogo **Gerenciador de Conexões MSMQ** para especificar o caminho do Serviço de Enfileiramento de Mensagens (também conhecido como MSMQ).  
  
 Para saber mais sobre o Gerenciador de Conexões MSMQ, consulte [Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md).  
  
> [!NOTE]  
>  O gerenciador de conexões MSMQ aceita filas públicas e privadas locais e filas públicas remotas. Não dá suporte a filas privadas remotas. Para obter uma solução alternativa que usa a tarefa Script, consulte [Enviando a uma fila de mensagens particular remota com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md).  
  
## Opções  
 **Nome**  
 Forneça um nome exclusivo para o gerenciador de conexões MSMQ no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Caminho**  
 Digite o caminho completo da fila de mensagens. O formato do caminho depende do tipo de fila.  
  
|Tipo de fila|Exemplo de caminho|  
|----------------|-----------------|  
|Público|\<nome do computador>\\<nome da fila\>|  
|Private|\<nome do computador>\Private$\\<nome da fila\>|  
  
 Você pode usar um "." para representar o computador local.  
  
 **Teste**  
 Depois de configurar o Gerenciador de Conexões MSMQ, confirme se a conexão é viável clicando em **Testar**.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  