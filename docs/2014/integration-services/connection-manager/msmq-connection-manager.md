---
title: Gerenciador de conexões MSMQ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 392b52142992baad8761ec1c25689db6726c8d67
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438393"
---
# <a name="msmq-connection-manager"></a>Gerenciador de conexões MSMQ
  Um gerenciador de conexões MSMQ permite que um pacote se conecte a uma fila de mensagens que usa Serviço de enfileiramento de mensagens (também conhecido como MSMQ). A tarefa Fila de Mensagens que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui, utiliza um gerenciador de conexões MSMQ.  
  
 Ao adicionar um gerenciador de conexões MSMQ a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibilizará uma conexão do MSMQ em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção de `Connections` no pacote. A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `MSMQ`.  
  
 É possível configurar um gerenciador de conexões MSMQ das seguintes maneiras:  
  
-   Fornecendo uma sequência de conexão.  
  
-   Fornecendo o caminho da fila de mensagem à qual se conectar.  
  
 O formato do caminho depende do tipo de fila, conforme mostrado na tabela a seguir.  
  
|Tipo de fila|Exemplo de caminho|  
|----------------|-----------------|  
|Público|\<computer name>\\Nome da fila de<\>|  
|Privado|\<computer name>Nome da fila do \Bytes privados $ \\<\>|  
  
 Você pode usar um ponto (.) para representar o computador local.  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>Configuração do gerenciador de conexões MSMQ  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões MSMQ](../msmq-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefa fila de mensagens](../control-flow/message-queue-task.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
