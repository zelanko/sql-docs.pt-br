---
title: "Editor da Tarefa Transferir Mensagens de Erro (p&#225;gina Mensagens) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transfererrormessagestask.errormessages.F1"
helpviewer_keywords: 
  - "Editor da Tarefa Transferir Mensagens de Erro"
ms.assetid: cb2226a0-3037-4fdf-966f-81eabc0da9cf
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Editor da Tarefa Transferir Mensagens de Erro (p&#225;gina Mensagens)
  Use a página **Mensagens** da caixa de diálogo **Editor da Tarefa Transferir Mensagens de Erro** para especificar as propriedades de cópia de uma ou mais mensagens de erro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidas pelo usuário de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. Para obter mais informações sobre essa tarefa, consulte [Transfer Error Messages Task](../../integration-services/control-flow/transfer-error-messages-task.md).  
  
## Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de destino.  
  
 **IfObjectExists**  
 Selecione se a tarefa deve substituir mensagens de erro definidas pelo usuário existentes, ignorar mensagens existentes ou causar falha se mensagens de erro de mesmo nome já existirem no servidor de destino.  
  
 **TransferAllErrorMessages**  
 Selecione se a tarefa deve copiar todas ou somente as mensagens especificadas definidas pelo usuário do servidor de origem para o servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**Verdadeiro**|Copia todas as mensagens definidas pelo usuário.|  
|**Falso**|Copia só as mensagens definidas pelo usuário especificadas.|  
  
 **ErrorMessagesList**  
 Clique no botão Procurar **(...)** para selecionar as mensagens de erro para copiar.  
  
> [!NOTE]  
>  É necessário especificar o **SourceConnection** antes que seja possível selecionar mensagens de erro para copiar.  
  
 **ErrorMessageLanguagesList**  
 Clique no botão Procurar **(...)** para selecionar os idiomas para os quais copiar mensagens de erro definidas pelo usuário para o servidor de destino. Uma versão us_english (página de código 1033) da mensagem deve estar no servidor de destino para que seja possível transferir versões da mensagem em outro idioma para esse servidor.  
  
> [!NOTE]  
>  É necessário especificar o **SourceConnection** antes que seja possível selecionar mensagens de erro para copiar.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor da Tarefa Transferir Mensagens de Erro &#40;Página Geral&#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-general-page.md)   
 [Gerenciador de conexões SMO](../../integration-services/connection-manager/smo-connection-manager.md)   
 [Editor da Tarefa Transferir Mensagens de Erro &#40;Página Geral&#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-general-page.md)   
 [Gerenciador de conexões SMO](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  