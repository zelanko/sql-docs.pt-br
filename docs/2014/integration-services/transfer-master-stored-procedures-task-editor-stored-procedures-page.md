---
title: Transferir o Editor da tarefa procedimentos armazenados mestres (páginas procedimentos armazenados) | Microsoft Docs
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f233f0730286a1623ee54c38084d07a2aba903e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054856"
---
# <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>Editor da Tarefa Transferir Procedimentos Armazenados Mestres (páginas Procedimentos Armazenados)
  Use a página **Procedimentos Armazenados** da caixa de diálogo **Editor da Tarefa Transferir Procedimentos Armazenados Mestres** para especificar propriedades para copiar um ou mais procedimentos armazenados definidos pelo usuário do banco de dados **mestre** em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para um banco de dados **mestre** em outra instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações sobre essa tarefa, consulte [Transfer Master Stored Procedures Task](control-flow/transfer-master-stored-procedures-task.md).  
  
> [!NOTE]  
>  Essa tarefa transfere apenas procedimentos armazenados definidos pelo usuário pertencentes ao **dbo** de um banco de dados **mestre** no servidor de origem para um banco de dados **mestre** no servidor de destino. Os usuários devem receber a permissão CREATE PROCEDURE no banco de dados **mestre** no servidor de destino ou devem ser membros da função de servidor fixa **sysadmin** no servidor de destino para criar procedimentos armazenados ali.  
  
## <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de destino.  
  
 **IfObjectExists**  
 Selecione como a tarefa deve manipular procedimentos armazenados definidos pelo usuário de nome idêntico a outros já existentes no banco de dados **mestre** no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**FailTask**|Haverá falha na tarefa se já existirem procedimentos armazenados de nome igual no banco de dados **mestre** no servidor de destino.|  
|**Overwrite**|A tarefa irá substituir os procedimentos armazenados de nome igual no banco de dados **mestre** no servidor de destino.|  
|**Skip**|A tarefa irá ignorar os procedimentos armazenados de nome igual já existentes no banco de dados **mestre** no servidor de destino.|  
  
 **TransferAllStoredProcedures**  
 Selecione se todos os procedimentos armazenados definidos pelo usuário no banco de dados **mestre** no servidor de origem devem ser copiados para o servidor de destino.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Verdadeiro**|Copiar todos os procedimentos armazenados definidos pelo usuário no banco de dados **mestre** .|  
|**Falso**|Copiar só os procedimentos armazenados especificados.|  
  
 **StoredProceduresList**  
 Selecione quais procedimentos armazenados definidos pelo usuário no banco de dados **mestre** no servidor de origem devem ser copiados para o banco de dados **mestre** no servidor de destino. Esta opção só fica disponível quando **TransferAllStoredProcedures** for definido como **False**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](control-flow/integration-services-tasks.md)   
 [Editor da Tarefa Transferir Procedimentos Armazenados Mestres &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expressões](expressions/expressions-page.md)   
 [Gerenciador de conexões SMO](connection-manager/smo-connection-manager.md)  
  
  
