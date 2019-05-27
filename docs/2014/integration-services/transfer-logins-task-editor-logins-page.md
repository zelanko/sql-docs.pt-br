---
title: Editor da tarefa logons (página logons) transferir | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ae8ebf56e4ae7c4fce3566cb7688d203b8ceb318
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054931"
---
# <a name="transfer-logins-task-editor-logins-page"></a>Editor da Tarefa Transferir Logons (página Logons)
  Use a página **Logons** da caixa de diálogo **Editor da Tarefa de Transferir Logons** para especificar as propriedades para copiar um ou mais logons [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de uma instância de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para outra. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Logons](control-flow/transfer-logins-task.md).  
  
> [!IMPORTANT]  
>  Quando a tarefa de Transferir Logons é executada, os logons são criados no servidor de destino com senhas aleatórias e as senhas são desabilitadas. Para usar esses logons, um membro da função de servidor fixa **sysadmin** deve alterar as senhas e habilitá-las. O logon do **sa** não pode ser transferido.  
  
## <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de destino.  
  
 **LoginsToTransfer**  
 Selecione os logons [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para copiar da fonte para o servidor de destino. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**AllLogins**|Todos os logons [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no servidor de origem serão copiados para o servidor de destino.|  
|**SelectedLogins**|Apenas os logons especificados com **LoginsList** serão copiados para o servidor de destino.|  
|**AllLoginsFromSelectedDatabases**|Todos os logons do banco de dados especificados com **DatabasesList** serão copiados para o servidor de destino.|  
  
 **LoginsList**  
 Selecione os logons no servidor de origem serão copiados para o servidor de destino. Esta opção somente está disponível quando **SelectedLogins** é selecionado para **LoginsToTransfer**.  
  
 **DatabasesList**  
 Selecione os logons no servidor de origem que serão copiados para o servidor de destino. Esta opção somente está disponível quando **AllLoginsFromSelectedDatabases** é selecionado para **LoginsToTransfer**.  
  
 **IfObjectExists**  
 Selecione como a tarefa deve tratar logons que tenham o mesmo nome já existente no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**FailTask**|A tarefa irá falhar se já existirem logons com o mesmo nome no servidor de destino.|  
|**Overwrite**|A tarefa irá substituir logons de mesmo nome no servidor de destino.|  
|**Skip**|A tarefa irá ignorar os logons de mesmo nome que existem no servidor de destino.|  
  
 **CopySids**  
 Selecione se os identificadores de segurança associados aos logons devem ser copiados para o servidor de destino. Será necessário definir**CopySids** para **True** se a tarefa Transferir Logons for usada junto com a tarefa Transferir Banco de Dados. Caso contrário, os logons copiados não serão reconhecidos pelo banco de dados transferido.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](control-flow/integration-services-tasks.md)   
 [Editor da Tarefa Transferir Logons &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expressões](expressions/expressions-page.md)   
 [Gerenciador de conexões SMO](connection-manager/smo-connection-manager.md)   
 [Senhas fortes](../relational-databases/security/strong-passwords.md)   
 [Considerações sobre segurança para uma instalação do SQL Server](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
