---
title: "Editor da Tarefa Transferir Procedimentos Armazenados Mestres (p&#225;ginas Procedimentos Armazenados) | Microsoft Docs"
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
  - "sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Transferir Procedimentos Armazenados Mestres"
ms.assetid: 5fcf171e-cc0b-4c24-8eb5-3a4b4775e64a
caps.latest.revision: 20
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 20
---
# Editor da Tarefa Transferir Procedimentos Armazenados Mestres (p&#225;ginas Procedimentos Armazenados)
  Use a página **Procedimentos Armazenados** da caixa de diálogo **Editor da Tarefa Transferir Procedimentos Armazenados Mestres** para especificar propriedades para copiar um ou mais procedimentos armazenados definidos pelo usuário do banco de dados **mestre** em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um banco de dados **mestre** em outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre essa tarefa, consulte [Transfer Master Stored Procedures Task](../../integration-services/control-flow/transfer-master-stored-procedures-task.md).  
  
> [!NOTE]  
>  Essa tarefa transfere apenas procedimentos armazenados definidos pelo usuário pertencentes ao **dbo** de um banco de dados **mestre** no servidor de origem para um banco de dados **mestre** no servidor de destino. Os usuários devem receber a permissão CREATE PROCEDURE no banco de dados **mestre** no servidor de destino ou devem ser membros da função de servidor fixa **sysadmin** no servidor de destino para criar procedimentos armazenados ali.  
  
## Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de destino.  
  
 **IfObjectExists**  
 Selecione como a tarefa deve manipular procedimentos armazenados definidos pelo usuário de nome idêntico a outros já existentes no banco de dados **mestre** no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**FailTask**|Haverá falha na tarefa se já existirem procedimentos armazenados de nome igual no banco de dados **mestre** no servidor de destino.|  
|**Overwrite**|A tarefa irá substituir os procedimentos armazenados de nome igual no banco de dados **mestre** no servidor de destino.|  
|**Skip**|A tarefa irá ignorar os procedimentos armazenados de nome igual já existentes no banco de dados **mestre** no servidor de destino.|  
  
 **TransferAllStoredProcedures**  
 Selecione se todos os procedimentos armazenados definidos pelo usuário no banco de dados **mestre** no servidor de origem devem ser copiados para o servidor de destino.  
  
|Value|Description|  
|-----------|-----------------|  
|**Verdadeiro**|Copiar todos os procedimentos armazenados definidos pelo usuário no banco de dados **mestre**.|  
|**Falso**|Copiar só os procedimentos armazenados especificados.|  
  
 **StoredProceduresList**  
 Selecione quais procedimentos armazenados definidos pelo usuário no banco de dados **mestre** no servidor de origem devem ser copiados para o banco de dados **mestre** no servidor de destino. Esta opção só fica disponível quando **TransferAllStoredProcedures** for definido como **False**.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor da Tarefa Transferir Procedimentos Armazenados Mestres &#40;página Geral&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-general-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)   
 [Gerenciador de conexões SMO](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  