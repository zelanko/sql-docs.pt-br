---
title: "Transferência de Editor de tarefa de mensagens de erro (página mensagens) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages Task Editor
ms.assetid: cb2226a0-3037-4fdf-966f-81eabc0da9cf
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8051e89dc6c319d13f51d086d702145548ea7e48
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-error-messages-task-editor-messages-page"></a>Editor da Tarefa Transferir Mensagens de Erro (página Mensagens)
  Use a página **Mensagens** da caixa de diálogo **Editor da Tarefa Transferir Mensagens de Erro** para especificar as propriedades de cópia de uma ou mais mensagens de erro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidas pelo usuário de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. Para obter mais informações sobre essa tarefa, consulte [Transfer Error Messages Task](../../integration-services/control-flow/transfer-error-messages-task.md).  
  
## <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um Gerenciador de conexão do SMO na lista ou clique em  **\<nova conexão... >** para criar uma nova conexão para o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um Gerenciador de conexão do SMO na lista ou clique em  **\<nova conexão... >** para criar uma nova conexão para o servidor de destino.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor de tarefa de mensagens de erro de transferência &#40; Página geral &#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-general-page.md)   
 [Gerenciador de Conexão do SMO](../../integration-services/connection-manager/smo-connection-manager.md)   
 [Editor de tarefa de mensagens de erro de transferência &#40; Página geral &#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-general-page.md)   
 [Gerenciador de Conexão do SMO](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  
