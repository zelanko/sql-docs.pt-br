---
title: Monitorar a Atividade de Trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, monitoring
- jobs [SQL Server Agent], monitoring
- monitoring [SQL Server], jobs
- activity monitoring [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- SQL Server Agent Job Activity Monitor
- SQL Server Agent jobs, monitoring
- performance [SQL Server], jobs
- current activity
ms.assetid: 71cb432b-631d-4b8b-9965-e731b3d8266d
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8bcfebba71f1cc1b022c0771b59ed3c1e9796c8b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="monitor-job-activity"></a>Monitorar Atividade do Trabalho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

É possível monitorar a atividade atual de todos os trabalhos definidos em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando o Monitor de Atividade do Trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="sql-server-agent-sessions"></a>Sessões do SQL Server Agent  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent cria uma nova sessão toda vez que o serviço é iniciado. Quando uma nova sessão é criada, a tabela **sysjobactivity** do banco de dados **msdb** é preenchida com todos os trabalhos definidos existentes. Essa tabela preserva a última atividade dos trabalhos quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é reiniciado. Cada sessão registra a atividade normal de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent do começo ao fim do trabalho. Informações sobre essas sessões são armazenadas na tabela **syssessions** do banco de dados **msdb** .  
  
## <a name="job-activity-monitor"></a>Monitor de Atividade do Trabalho  
O Monitor de Atividade do Trabalho permite exibir a tabela **sysjobactivity** usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. É possível visualizar todos os trabalhos no servidor ou definir filtros para limitar o número de trabalhos exibidos. Você também pode classificar as informações do trabalho, clicando no título de uma coluna na grade do **Atividade de Trabalho do Agente** . Por exemplo, selecionando o título de coluna **Última Execução** , é possível exibir os trabalhos na ordem em que foram executados pela última vez. Clicando novamente no cabeçalho da coluna, os trabalhos são classificados em ordem crescente ou decrescente segundo as datas de suas últimas execuções.  
  
Usando o Monitor de Atividade do Trabalho, você pode executar as seguintes tarefas:  
  
-   Iniciar e interromper trabalhos.  
  
-   Exibir propriedades do trabalho.  
  
-   Exibir o histórico de um trabalho específico.  
  
-   Atualizar as informações na grade de **Atividade do Trabalho do Agente** manualmente ou definir um intervalo de atualização automática, clicando em **Exibir configurações de atualização**.  
  
Use o Monitor de Atividade do Trabalho quando quiser descobrir quais trabalhos estão agendados para execução, o último resultado de trabalhos executados durante a sessão atual e quais trabalhos estão em execução ou ociosos atualmente. Se o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent falhar de forma inesperada, você poderá determinar quais trabalhos estavam no meio de sua execução, examinando a sessão anterior no Monitor de Atividade do Trabalho.  
  
Para abrir o Monitor de Atividade do Trabalho, expanda **SQL Server Agent** no Pesquisador de Objetos do [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] , clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e clique em **Exibir Atividade do Trabalho**.  
  
Você também pode exibir a atividade de trabalhos da sessão atual, usando o procedimento armazenado **sp_help_jobactivity**.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como exibir o estado de tempo de execução de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Exibir Atividade do Trabalho](../../ssms/agent/view-job-activity.md)|  
  
## <a name="see-also"></a>Consulte Também  
[Exibir Atividade do Trabalho](../../ssms/agent/view-job-activity.md)  
[sysjobactivity (Transact-SQL)](http://msdn.microsoft.com/en-us/fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e)  
[syssessions (Transact-SQL)](http://msdn.microsoft.com/en-us/187819b6-c7f4-4a26-b74c-0a89e96695cf)  
[sp_help_jobactivity (Transact-SQL)](http://msdn.microsoft.com/en-us/d344864f-b4d3-46b1-8933-b81dec71f511)  
  
