---
title: "Transferência de logons Editor da tarefa (página logons) | Microsoft Docs"
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
- sql13.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cdae4242ff131376f8aba2bd4a1ec4fc08170ecd
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-logins-task-editor-logins-page"></a>Editor da Tarefa Transferir Logons (página Logons)
  Use a página **Logons** da caixa de diálogo **Editor da Tarefa de Transferir Logons** para especificar as propriedades para copiar um ou mais logons [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Logons](../../integration-services/control-flow/transfer-logins-task.md).  
  
> [!IMPORTANT]  
>  Quando a tarefa de Transferir Logons é executada, os logons são criados no servidor de destino com senhas aleatórias e as senhas são desabilitadas. Para usar esses logons, um membro da função de servidor fixa **sysadmin** deve alterar as senhas e habilitá-las. O logon do **sa** não pode ser transferido.  
  
## <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um Gerenciador de conexão do SMO na lista ou clique em  **\<nova conexão... >** para criar uma nova conexão para o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um Gerenciador de conexão do SMO na lista ou clique em  **\<nova conexão... >** para criar uma nova conexão para o servidor de destino.  
  
 **LoginsToTransfer**  
 Selecione os logons [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para copiar da fonte para o servidor de destino. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**AllLogins**|Todos os logons [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor de origem serão copiados para o servidor de destino.|  
|**SelectedLogins**|Apenas os logons especificados com **LoginsList** serão copiados para o servidor de destino.|  
|**AllLoginsFromSelectedDatabases**|Todos os logons do banco de dados especificados com **DatabasesList** serão copiados para o servidor de destino.|  
  
 **LoginsList**  
 Selecione os logons no servidor de origem serão copiados para o servidor de destino. Esta opção somente está disponível quando **SelectedLogins** é selecionado para **LoginsToTransfer**.  
  
 **DatabasesList**  
 Selecione os logons no servidor de origem que serão copiados para o servidor de destino. Esta opção somente está disponível quando **AllLoginsFromSelectedDatabases** é selecionado para **LoginsToTransfer**.  
  
 **IfObjectExists**  
 Selecione como a tarefa deve tratar logons que tenham o mesmo nome já existente no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**FailTask**|A tarefa irá falhar se já existirem logons com o mesmo nome no servidor de destino.|  
|**Overwrite**|A tarefa irá substituir logons de mesmo nome no servidor de destino.|  
|**Skip**|A tarefa irá ignorar os logons de mesmo nome que existem no servidor de destino.|  
  
 **CopySids**  
 Selecione se os identificadores de segurança associados aos logons devem ser copiados para o servidor de destino. Será necessário definir**CopySids** para **True** se a tarefa Transferir Logons for usada junto com a tarefa Transferir Banco de Dados. Caso contrário, os logons copiados não serão reconhecidos pelo banco de dados transferido.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor da tarefa transferir logons &#40; Página geral &#41;](../../integration-services/control-flow/transfer-logins-task-editor-general-page.md)   
 [Página expressões](../../integration-services/expressions/expressions-page.md)   
 [Gerenciador de Conexão do SMO](../../integration-services/connection-manager/smo-connection-manager.md)   
 [Senhas fortes](../../relational-databases/security/strong-passwords.md)   
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
