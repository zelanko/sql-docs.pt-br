---
title: "Editor da Tarefa Fila de Mensagens (p&#225;gina Geral) | Microsoft Docs"
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
  - "sql13.dts.designer.msgqueuetask.general.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Fila de Mensagens"
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Editor da Tarefa Fila de Mensagens (p&#225;gina Geral)
  Use a **página Geral** da caixa de diálogo do **Editor da Tarefa Fila de Mensagens** para nomear e descrever a tarefa Fila de Mensagens, especificar o formato da mensagem e indicar se a tarefa envia ou recebe mensagens.  
  
 Para obter informações sobre essa tarefa, consulte [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Fila de Mensagens. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Description**  
 Digite uma descrição para a tarefa Fila de Mensagens.  
  
 **Use2000Format**  
 Indique se deseja usar o formato 2000 do serviço de enfileiramento de mensagens (também conhecido como MSMQ). O padrão é **False**.  
  
 **MSMQConnection**  
 Selecione um gerenciador de conexões de MSMQ existente ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados**: [Gerenciador de conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md), [Editor do Gerenciador de Conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **Mensagem**  
 Especifique se a tarefa Fila de Mensagens envia ou recebe mensagens. Se você selecionar **Enviar mensagem**, será listada a página Enviar no painel esquerdo da caixa de diálogo; se você selecionar **Receber mensagem**, será listada a página Receber. Por padrão, esse valor está definido como **Enviar mensagem**.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa Fila de Mensagens &#40;Página Receber&#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [Editor da Tarefa Fila de Mensagens &#40;Página Enviar&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  