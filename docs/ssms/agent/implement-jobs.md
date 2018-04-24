---
title: Implementar Trabalhos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0f16a99dd009d3e3e7e31349100aa26de82c890b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="implement-jobs"></a>Implementar trabalhos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

É possível usar trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para automatizar tarefas administrativas de rotina e executá-las recorrentemente, tornando a administração mais eficaz.  
  
Um trabalho é uma série especificada de operações executadas sequencialmente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Um trabalho pode realizar uma ampla gama de atividades, tais como a execução de scripts [!INCLUDE[tsql](../../includes/tsql_md.md)] , aplicativos de linha de comando, scripts Microsoft ActiveX, pacotes do Integration Services, comandos e consultas do Analysis Services ou tarefas de replicação. Os trabalhos podem executar tarefas repetitivas ou agendáveis, bem como notificar usuários automaticamente sobre o status do trabalho por meio de alertas, desse modo simplificando bastante a administração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
É possível executar um trabalho manualmente ou configurá-lo para executar de acordo com uma agenda ou em resposta a alertas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Contém informações sobre como criar trabalhos e atribuir propriedade.|[Criar trabalhos](../../ssms/agent/create-jobs.md)|  
|Contém informações sobre como organizar trabalhos em categorias.|[Organizar trabalhos](../../ssms/agent/organize-jobs.md)|  
|Contém informações sobre os diferentes tipos de etapas de trabalho que podem ser criadas e como gerenciá-las.|[Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)|  
|Contém informações sobre como definir o início e a frequência da execução de trabalhos.|[Criar e anexar agendas para trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|Contém informações sobre como executar trabalhos manualmente (sem uma agenda).|[Executar Trabalhos](../../ssms/agent/run-jobs.md)|  
|Contém informações sobre como configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para responder a trabalhos. Por exemplo, você pode configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para notificar administradores quando os trabalhos forem concluídos.|[Especificar respostas de trabalho](../../ssms/agent/specify-job-responses.md)|  
|Contém informações sobre como exibir trabalhos existentes, seu histórico quando executado, e como modificá-los.|[Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)|  
|Contém informações sobre como excluir trabalhos.|[Excluir trabalhos](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>Consulte Também  
[Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
