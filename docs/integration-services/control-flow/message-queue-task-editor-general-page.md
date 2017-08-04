---
title: "Editor de tarefa de fila de mensagens (página geral) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msgqueuetask.general.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 25313cc6decaea073409143e468621a1ed40993c
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="message-queue-task-editor-general-page"></a>Editor da Tarefa Fila de Mensagens (página Geral)
  Use a **página Geral** da caixa de diálogo do **Editor da Tarefa Fila de Mensagens** para nomear e descrever a tarefa Fila de Mensagens, especificar o formato da mensagem e indicar se a tarefa envia ou recebe mensagens.  
  
 Para obter informações sobre essa tarefa, consulte [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Fila de Mensagens. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Description**  
 Digite uma descrição para a tarefa Fila de Mensagens.  
  
 **Use2000Format**  
 Indique se deseja usar o formato 2000 do serviço de enfileiramento de mensagens (também conhecido como MSMQ). O padrão é **False**.  
  
 **MSMQConnection**  
 Selecione um Gerenciador de conexão do MSMQ existente ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados**: [Gerenciador de conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md), [Editor do Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **Mensagem**  
 Especifique se a tarefa Fila de Mensagens envia ou recebe mensagens. Se você selecionar **Enviar mensagem**, será listada a página Enviar no painel esquerdo da caixa de diálogo; se você selecionar **Receber mensagem**, será listada a página Receber. Por padrão, esse valor está definido como **Enviar mensagem**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de tarefa da fila de mensagens &#40; Receber página &#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [Editor de tarefa da fila de mensagens &#40; Enviar página &#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  
