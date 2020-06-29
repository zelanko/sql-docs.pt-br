---
title: Editor da tarefa Transferir procedimentos armazenados mestres (página procedimentos armazenados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: 5fcf171e-cc0b-4c24-8eb5-3a4b4775e64a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0cd0b269c0ced445017d573cfad08a767d5f2008
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439983"
---
# <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>Editor da Tarefa Transferir Procedimentos Armazenados Mestres (páginas Procedimentos Armazenados)
  Use a página **Procedimentos Armazenados** da caixa de diálogo **Editor da Tarefa Transferir Procedimentos Armazenados Mestres** para especificar propriedades para copiar um ou mais procedimentos armazenados definidos pelo usuário do banco de dados **mestre** em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para um banco de dados **mestre** em outra instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações sobre essa tarefa, consulte [Transfer Master Stored Procedures Task](control-flow/transfer-master-stored-procedures-task.md).  
  
> [!NOTE]  
>  Essa tarefa transfere apenas procedimentos armazenados definidos pelo usuário pertencentes ao **dbo** de um banco de dados **mestre** no servidor de origem para um banco de dados **mestre** no servidor de destino. Os usuários devem receber a permissão CREATE PROCEDURE no banco de dados **mestre** no servidor de destino ou devem ser membros da função de servidor fixa **sysadmin** no servidor de destino para criar procedimentos armazenados ali.  
  
## <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um Gerenciador de conexões SMO na lista ou clique **\<New connection...>** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um Gerenciador de conexões SMO na lista ou clique **\<New connection...>** para criar uma nova conexão com o servidor de destino.  
  
 **IfObjectExists**  
 Selecione como a tarefa deve manipular procedimentos armazenados definidos pelo usuário de nome idêntico a outros já existentes no banco de dados **mestre** no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**FailTask**|Haverá falha na tarefa se já existirem procedimentos armazenados de nome igual no banco de dados **mestre** no servidor de destino.|  
|**Overwrite**|A tarefa irá substituir os procedimentos armazenados de nome igual no banco de dados **mestre** no servidor de destino.|  
|**Ignorar**|A tarefa irá ignorar os procedimentos armazenados de nome igual já existentes no banco de dados **mestre** no servidor de destino.|  
  
 **TransferAllStoredProcedures**  
 Selecione se todos os procedimentos armazenados definidos pelo usuário no banco de dados **mestre** no servidor de origem devem ser copiados para o servidor de destino.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**True**|Copiar todos os procedimentos armazenados definidos pelo usuário no banco de dados **mestre** .|  
|**For**|Copiar só os procedimentos armazenados especificados.|  
  
 **StoredProceduresList**  
 Selecione quais procedimentos armazenados definidos pelo usuário no banco de dados **mestre** no servidor de origem devem ser copiados para o banco de dados **mestre** no servidor de destino. Esta opção só fica disponível quando **TransferAllStoredProcedures** for definido como **False**.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas de Integration Services](control-flow/integration-services-tasks.md)   
 [Editor da tarefa Transferir procedimentos armazenados mestres &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página de expressões](expressions/expressions-page.md)   
 [Gerenciador de Conexões SMO](connection-manager/smo-connection-manager.md)  
  
  
