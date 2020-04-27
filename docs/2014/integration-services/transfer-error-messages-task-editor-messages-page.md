---
title: Editor da tarefa transferir mensagens de erro (página mensagens) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages Task Editor
ms.assetid: cb2226a0-3037-4fdf-966f-81eabc0da9cf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f753aaddbd2647b1d8874b0d34db415f75aa99b9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66055035"
---
# <a name="transfer-error-messages-task-editor-messages-page"></a>Editor da Tarefa Transferir Mensagens de Erro (página Mensagens)
  Use a página **Mensagens** da caixa de diálogo **Editor da Tarefa Transferir Mensagens de Erro** para especificar as propriedades de cópia de uma ou mais mensagens de erro [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] definidas pelo usuário de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para outra. Para obter mais informações sobre essa tarefa, consulte [Transfer Error Messages Task](control-flow/transfer-error-messages-task.md).  
  
## <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um Gerenciador de conexões Smo na lista ou clique em ** \<nova conexão... >** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um Gerenciador de conexões Smo na lista ou clique em ** \<nova conexão... >** para criar uma nova conexão com o servidor de destino.  
  
 **IfObjectExists**  
 Selecione se a tarefa deve substituir mensagens de erro definidas pelo usuário existentes, ignorar mensagens existentes ou causar falha se mensagens de erro de mesmo nome já existirem no servidor de destino.  
  
 **TransferAllErrorMessages**  
 Selecione se a tarefa deve copiar todas ou somente as mensagens especificadas definidas pelo usuário do servidor de origem para o servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**True**|Copia todas as mensagens definidas pelo usuário.|  
|**For**|Copia só as mensagens definidas pelo usuário especificadas.|  
  
 **ErrorMessagesList**  
 Clique no botão Procurar **(...)** para selecionar as mensagens de erro para copiar.  
  
> [!NOTE]  
>  É necessário especificar o **SourceConnection** antes que seja possível selecionar mensagens de erro para copiar.  
  
 **ErrorMessageLanguagesList**  
 Clique no botão Procurar **(...)** para selecionar os idiomas para os quais copiar mensagens de erro definidas pelo usuário para o servidor de destino. Uma versão us_english (página de código 1033) da mensagem deve estar no servidor de destino para que seja possível transferir versões da mensagem em outro idioma para esse servidor.  
  
> [!NOTE]  
>  É necessário especificar o **SourceConnection** antes que seja possível selecionar mensagens de erro para copiar.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas de Integration Services](control-flow/integration-services-tasks.md)   
 [Editor da tarefa transferir mensagens de erro &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Gerenciador de conexões SMO](connection-manager/smo-connection-manager.md)   
 [Editor da tarefa transferir mensagens de erro &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [gerenciador de conexões SMO](connection-manager/smo-connection-manager.md)  
  
  
