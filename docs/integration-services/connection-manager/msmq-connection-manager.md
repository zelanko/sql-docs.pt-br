---
title: "Gerenciador de Conexão do MSMQ | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 0e028f9f648acc18d56dc05262adccbbc52f8f7e
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="msmq-connection-manager"></a>Gerenciador de conexões MSMQ
  Um gerenciador de conexões MSMQ permite que um pacote se conecte a uma fila de mensagens que usa Serviço de enfileiramento de mensagens (também conhecido como MSMQ). A tarefa Fila de Mensagens que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui, utiliza um gerenciador de conexões MSMQ.  
  
 Ao adicionar um gerenciador de conexões MSMQ a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibilizará uma conexão do MSMQ em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** no pacote. A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **MSMQ**.  
  
 É possível configurar um gerenciador de conexões MSMQ das seguintes maneiras:  
  
-   Fornecendo uma sequência de conexão.  
  
-   Fornecendo o caminho da fila de mensagem à qual se conectar.  
  
 O formato do caminho depende do tipo de fila, conforme mostrado na tabela a seguir.  
  
|Tipo de fila|Exemplo de caminho|  
|----------------|-----------------|  
|Público|\<nome do computador >\\< nome da fila\>|  
|Private|\<nome do computador > \Private$\\< nome da fila\>|  
  
 Você pode usar um ponto (.) para representar o computador local.  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>Configuração do gerenciador de conexões MSMQ  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="msmq-connection-manager-editor"></a>Editor do Gerenciador de Conexões MSMQ
  Use a caixa de diálogo **Gerenciador de Conexões MSMQ** para especificar o caminho do Serviço de Enfileiramento de Mensagens (também conhecido como MSMQ).  
  
 Para saber mais sobre o Gerenciador de Conexões MSMQ, consulte [Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md).  
  
> [!NOTE]  
>  O gerenciador de conexões MSMQ aceita filas públicas e privadas locais e filas públicas remotas. Não dá suporte a filas privadas remotas. Para obter uma solução alternativa que usa a tarefa Script, consulte [Enviando a uma fila de mensagens particular remota com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md).  
  
### <a name="options"></a>Opções  
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
 [Tarefa Fila de Mensagens](../../integration-services/control-flow/message-queue-task.md)   
 [Integration Services &#40; SSIS &#41; Conexões](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  

