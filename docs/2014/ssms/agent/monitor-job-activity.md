---
title: Monitorar a Atividade de Trabalho | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5088e029e90b4556c1559f8c948e8a8734762749
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85001878"
---
# <a name="monitor-job-activity"></a>Monitorar Atividade do Trabalho
  É possível monitorar a atividade atual de todos os trabalhos definidos em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Monitor de Atividade do Trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="sql-server-agent-sessions"></a>Sessões do SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent cria uma nova sessão toda vez que o serviço é iniciado. Quando uma nova sessão é criada, a tabela **sysjobactivity** do banco de dados **msdb** é preenchida com todos os trabalhos definidos existentes. Essa tabela preserva a última atividade dos trabalhos quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é reiniciado. Cada sessão registra a atividade normal de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent do começo ao fim do trabalho. Informações sobre essas sessões são armazenadas na tabela **syssessions** do banco de dados **msdb** .  
  
## <a name="job-activity-monitor"></a>Monitor de Atividade do Trabalho  
 O Monitor de Atividade do Trabalho permite exibir a tabela **sysjobactivity** usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. É possível visualizar todos os trabalhos no servidor ou definir filtros para limitar o número de trabalhos exibidos. Você também pode classificar as informações do trabalho, clicando no título de uma coluna na grade do **Atividade de Trabalho do Agente** . Por exemplo, selecionando o título de coluna **Última Execução** , é possível exibir os trabalhos na ordem em que foram executados pela última vez. Clicando novamente no cabeçalho da coluna, os trabalhos são classificados em ordem crescente ou decrescente segundo as datas de suas últimas execuções.  
  
 Usando o Monitor de Atividade do Trabalho, você pode executar as seguintes tarefas:  
  
-   Iniciar e interromper trabalhos.  
  
-   Exibir propriedades do trabalho.  
  
-   Exibir o histórico de um trabalho específico.  
  
-   Atualizar as informações na grade de **Atividade do Trabalho do Agente** manualmente ou definir um intervalo de atualização automática, clicando em **Exibir configurações de atualização**.  
  
 Use o Monitor de Atividade do Trabalho quando quiser descobrir quais trabalhos estão agendados para execução, o último resultado de trabalhos executados durante a sessão atual e quais trabalhos estão em execução ou ociosos atualmente. Se o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent falhar de forma inesperada, você poderá determinar quais trabalhos estavam no meio de sua execução, examinando a sessão anterior no Monitor de Atividade do Trabalho.  
  
 Para abrir o Monitor de Atividade do Trabalho, expanda **SQL Server Agent** no Pesquisador de Objetos do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e clique em **Exibir Atividade do Trabalho**.  
  
 Você também pode exibir a atividade de trabalhos da sessão atual, usando o procedimento armazenado **sp_help_jobactivity**.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como exibir o estado de runtime de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Exibir Atividade do Trabalho](view-job-activity.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir atividade do trabalho](view-job-activity.md)   
 [dbo.sysjobactivity &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobactivity-transact-sql)   
 [dbo.syssessões &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-syssessions-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_help_jobactivity](/sql/relational-databases/system-stored-procedures/sp-help-jobactivity-transact-sql)  
  
  
