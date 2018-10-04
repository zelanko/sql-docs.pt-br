---
title: Gerenciador de conexões MSMQ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a1501af4a26c0e039df3113a719a61e1e2c3f40a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135036"
---
# <a name="msmq-connection-manager"></a>Gerenciador de conexões MSMQ
  Um gerenciador de conexões MSMQ permite que um pacote se conecte a uma fila de mensagens que usa Serviço de enfileiramento de mensagens (também conhecido como MSMQ). A tarefa Fila de Mensagens que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui, utiliza um gerenciador de conexões MSMQ.  
  
 Quando você adiciona um Gerenciador de conexão do MSMQ a um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria uma conexão Gerenciador que resolverá uma conexão do MSMQ em tempo de execução, define propriedades do Gerenciador da conexão e adiciona o Gerenciador de conexão para o `Connections` coleta no pacote. O `ConnectionManagerType` propriedade do Gerenciador de conexão é definida como `MSMQ`.  
  
 É possível configurar um gerenciador de conexões MSMQ das seguintes maneiras:  
  
-   Fornecendo uma sequência de conexão.  
  
-   Fornecendo o caminho da fila de mensagem à qual se conectar.  
  
 O formato do caminho depende do tipo de fila, conforme mostrado na tabela a seguir.  
  
|Tipo de fila|Exemplo de caminho|  
|----------------|-----------------|  
|Público|\<nome do computador>\\<nome da fila\>|  
|Private|\<nome do computador>\Private$\\<nome da fila\>|  
  
 Você pode usar um ponto (.) para representar o computador local.  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>Configuração do gerenciador de conexões MSMQ  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões MSMQ](../msmq-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um Gerenciador de conexão programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa fila de mensagens](../control-flow/message-queue-task.md)   
 [Serviços de integração &#40;SSIS&#41; conexões](integration-services-ssis-connections.md)  
  
  
