---
title: Criar um alerta SQL Server Agent com o provedor WMI
description: Crie um SQL Server Agent alerta que responda a eventos específicos. Esse alerta simples salva eventos de grafo de Deadlock XML em uma tabela para análise posterior.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SQL Server Agent [WMI]
- WMI Provider for Server Events, samples
- sample applications [WMI]
ms.assetid: d44811c7-cd46-4017-b284-c863ca088e8f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a1678379c2120ba4f2edbc2868d5651cbf403587
ms.sourcegitcommit: bf5e9cb3a2caa25d0a37f401b3806b7baa5adea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85295409"
---
# <a name="sample-creating-a-sql-server-agent-alert-with-the-wmi-provider"></a>Exemplo: Criar um alerta do SQL Server Agent com o Provedor WMI
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Uma forma comum de usar o Provedor de eventos de WMI é criar alertas do SQL Server Agent que respondem a eventos específicos. O seguinte exemplo apresenta um alerta simples que salva eventos de gráfico de deadlock XML em uma tabela para análise posterior. O SQL Server Agent envia uma solicitação WQL, recebe eventos WMI, e executa um trabalho em resposta ao evento. Observe que, embora vários objetos do Service Broker estejam envolvidos no processamento da mensagem de notificação, o Provedor de eventos de WMI manipula os detalhes da criação e do gerenciamento desses objetos.  
  
## <a name="example"></a>Exemplo  
 Primeiro, uma tabela é criada no banco de dados `AdventureWorks` para conter o evento de gráfico de deadlock. A tabela contém duas colunas: a coluna `AlertTime` contém a hora em que o alerta é executado e a coluna `DeadlockGraph`, o documento XML que contém o gráfico de deadlock.  
  
 Então, o alerta é criado. Primeiro, o script cria o trabalho que o alerta irá executar, depois adiciona uma etapa de trabalho ao trabalho e direciona o trabalho para a instância atual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Então, o script cria o alerta.  
  
 A etapa de trabalho recupera a propriedade **TextData** da instância de evento WMI e insere esse valor na coluna **DeadlockGraph** da tabela **DeadlockEvents** . Observe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte implicitamente a cadeia de caracteres para o formato XML. Como a etapa de trabalho usa o subsistema [!INCLUDE[tsql](../../includes/tsql-md.md)], ela não especifica um proxy.  
  
 O alerta executa o trabalho sempre que um evento de rastreamento do grafo deadlock é registrado. Para um alerta de WMI, o SQL Server Agent cria uma consulta de notificação que usa o namespace e a instrução WQL especificados. Para esse alerta, o SQL Server Agent monitora a instância padrão no computador local. A instrução WQL solicita quaisquer eventos `DEADLOCK_GRAPH` na instância padrão. Para alterar a instância que o alerta monitora, substitua o nome de instância para `MSSQLSERVER` no `@wmi_namespace` para o alerta.  
  
> [!NOTE]  
>  Para SQL Server Agent receber eventos WMI, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve estar habilitado no **msdb** e no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
USE AdventureWorks ;  
GO  
  
IF OBJECT_ID('DeadlockEvents', 'U') IS NOT NULL  
BEGIN  
    DROP TABLE DeadlockEvents ;  
END ;  
GO  
  
CREATE TABLE DeadlockEvents  
    (AlertTime DATETIME, DeadlockGraph XML) ;  
GO  
-- Add a job for the alert to run.  
  
EXEC  msdb.dbo.sp_add_job @job_name=N'Capture Deadlock Graph',   
    @enabled=1,   
    @description=N'Job for responding to DEADLOCK_GRAPH events' ;  
GO  
  
-- Add a jobstep that inserts the current time and the deadlock graph into  
-- the DeadlockEvents table.  
  
EXEC msdb.dbo.sp_add_jobstep  
    @job_name = N'Capture Deadlock Graph',  
    @step_name=N'Insert graph into LogEvents',  
    @step_id=1,   
    @on_success_action=1,   
    @on_fail_action=2,   
    @subsystem=N'TSQL',   
    @command= N'INSERT INTO DeadlockEvents  
                (AlertTime, DeadlockGraph)  
                VALUES (getdate(), N''$(ESCAPE_SQUOTE(WMI(TextData)))'')',  
    @database_name=N'AdventureWorks' ;  
GO  
  
-- Set the job server for the job to the current instance of SQL Server.  
  
EXEC msdb.dbo.sp_add_jobserver @job_name = N'Capture Deadlock Graph' ;  
GO  
  
-- Add an alert that responds to all DEADLOCK_GRAPH events for  
-- the default instance. To monitor deadlocks for a different instance,  
-- change MSSQLSERVER to the name of the instance.  
  
EXEC msdb.dbo.sp_add_alert @name=N'Respond to DEADLOCK_GRAPH',   
@wmi_namespace=N'\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER',   
    @wmi_query=N'SELECT * FROM DEADLOCK_GRAPH',   
    @job_name='Capture Deadlock Graph' ;  
GO  
```  
  
## <a name="testing-the-sample"></a>Testando o exemplo  
 Para ver a execução do trabalho, provoque um deadlock. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , abra duas guias de **consulta SQL** e conecte ambas as consultas à mesma instância. Execute o seguinte script em um das guias de consulta. Este script produz um conjunto de resultados e é encerrado.  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 Execute o script a seguir na segunda guia de consulta. Esse script produz um conjunto de resultados e, em seguida, os bloqueia, aguardando a aquisição de um bloqueio `Production.Product` .  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 Execute o script a seguir na primeira guia de consulta. Esse script é bloqueado, aguardando a aquisição de um bloqueio `Production.Location` . Depois de um tempo limite curto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escolherá este script ou o script no exemplo como a vítima de deadlock e encerrará a transação.  
  
```  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
```  
  
 Depois de provocar o deadlock, aguarde algum tempo para o SQL Server Agent ativar o alerta e executar o trabalho. Examine o conteúdo da tabela `DeadlockEvents` executando o seguinte script:  
  
```  
SELECT * FROM DeadlockEvents ;  
GO  
```  
  
 A coluna `DeadlockGraph` deve conter um documento XML que mostra todas as propriedades do evento do gráfico de deadlock.  
  
## <a name="see-also"></a>Consulte Também  
 [Provedor WMI para conceitos de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
