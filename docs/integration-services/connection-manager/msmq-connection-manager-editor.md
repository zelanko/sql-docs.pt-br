---
title: "Editor do Gerenciador de Conexão MSMQ | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- MSMQ Connection Manager Editor
ms.assetid: ef842cb4-82da-4550-85fe-9bedbc1e77c7
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 21921237e1575c6d7723c86ae5decc84cfb19ea5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="msmq-connection-manager-editor"></a>Editor do Gerenciador de Conexões MSMQ
  Use a caixa de diálogo **Gerenciador de Conexões MSMQ** para especificar o caminho do Serviço de Enfileiramento de Mensagens (também conhecido como MSMQ).  
  
 Para saber mais sobre o Gerenciador de Conexões MSMQ, consulte [Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md).  
  
> [!NOTE]  
>  O gerenciador de conexões MSMQ aceita filas públicas e privadas locais e filas públicas remotas. Não dá suporte a filas privadas remotas. Para obter uma solução alternativa que usa a tarefa Script, consulte [Enviando a uma fila de mensagens particular remota com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md).  
  
## <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para o gerenciador de conexões MSMQ no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Caminho**  
 Digite o caminho completo da fila de mensagens. O formato do caminho depende do tipo de fila.  
  
|Tipo de fila|Exemplo de caminho|  
|----------------|-----------------|  
|Público|\<nome do computador >\\< nome da fila\>|  
|Private|\<nome do computador > \Private$\\< nome da fila\>|  
  
 Você pode usar um "." para representar o computador local.  
  
 **Teste**  
 Depois de configurar o Gerenciador de Conexões MSMQ, confirme se a conexão é viável clicando em **Testar**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  
