---
title: "Editor da Tarefa Transferir Trabalhos (p&#225;gina Trabalhos) | Microsoft Docs"
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
  - "sql13.dts.designer.transferjobstask.jobs.f1"
helpviewer_keywords: 
  - "Editor de Tarefa Transferir Trabalhos"
ms.assetid: e72b1dc7-8cda-4ee6-abb5-d438370f04df
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Editor da Tarefa Transferir Trabalhos (p&#225;gina Trabalhos)
  Use a página **Trabalhos** da caixa de diálogo **Editor da Tarefa de Transferir Trabalhos** para especificar as propriedades para cópia de um ou mais trabalhos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. Para obter mais informações sobre a tarefa Transferir Trabalhos, consulte [Transfer Jobs Task](../../integration-services/control-flow/transfer-jobs-task.md).  
  
> [!NOTE]  
>  Para acessar trabalhos no servidor de origem, é necessário que os usuários sejam membros pelo menos da função do banco de dados fixa **SQLAgentUserRole** no servidor. Para criar trabalhos no servidor de destino com êxito, é necessário que o usuário seja um membro da função de servidor fixa **sysadmin** ou uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e suas permissões, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de destino.  
  
 **TransferAllJobs**  
 Selecione se a tarefa deve copiar todas ou apenas os trabalhos de Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados do servidor de origem para o servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**Verdadeiro**|Copia todas as tarefas.|  
|**Falso**|Copia apenas os trabalhos especificados.|  
  
 **JobsList**  
 Clique no botão Procurar **(...)** para selecionar os trabalhos a serem copiados. Pelo menos um trabalho deve ser selecionado.  
  
> [!NOTE]  
>  Especifique a **SourceConnection** antes de selecionar trabalhos para copiar.  
  
 A opção **JobsList** não estará disponível quando **TransferAllJobs** for definido como **True**.  
  
 **IfObjectExists**  
 Selecione como a tarefa deve tratar trabalhos que tenham o mesmo nome já existente no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**FailTask**|A tarefa irá falhar se já existirem trabalhos com o mesmo nome no servidor de destino.|  
|**Overwrite**|A tarefa irá substituir trabalhos de mesmo nome no servidor de destino.|  
|**Skip**|A tarefa irá ignorar os trabalhos de mesmo nome que existem no servidor de destino.|  
  
 **EnableJobsAtDestination**  
 Selecione se os trabalhos copiados para o servidor de destino devem ser habilitados.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**Verdadeiro**|Habilita trabalhos no servidor de destino.|  
|**Falso**|Desabilita trabalhos no servidor de destino.|  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor da Tarefa Transferir Trabalhos &#40;Página Geral&#41;](../../integration-services/control-flow/transfer-jobs-task-editor-general-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)   
 [Gerenciador de conexões SMO](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  