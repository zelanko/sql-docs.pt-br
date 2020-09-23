---
description: Implementar trabalhos
title: Implementar trabalhos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 503f2a0ab50d38b70a1002f3a12ad6508479d755
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463054"
---
# <a name="implement-jobs"></a>Implementar trabalhos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

É possível usar trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para automatizar tarefas administrativas de rotina e executá-las recorrentemente, tornando a administração mais eficaz.  
  
Um trabalho é uma série especificada de operações executadas sequencialmente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Um trabalho pode realizar uma ampla gama de atividades, tais como a execução de scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , aplicativos de linha de comando, scripts Microsoft ActiveX, pacotes do Integration Services, comandos e consultas do Analysis Services ou tarefas de replicação. Os trabalhos podem executar tarefas repetitivas ou agendáveis, bem como notificar usuários automaticamente sobre o status do trabalho por meio de alertas, desse modo simplificando bastante a administração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
É possível executar um trabalho manualmente ou configurá-lo para executar de acordo com uma agenda ou em resposta a alertas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição|Tópico|  
|-|-|   
|Contém informações sobre como criar trabalhos e atribuir propriedade.|[Criar trabalhos](../../ssms/agent/create-jobs.md)|  
|Contém informações sobre como organizar trabalhos em categorias.|[organizar trabalhos](../../ssms/agent/organize-jobs.md)|  
|Contém informações sobre os diferentes tipos de etapas de trabalho que podem ser criadas e como gerenciá-las.|[Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)|  
|Contém informações sobre como definir o início e a frequência da execução de trabalhos.|[Criar e anexar agendas para trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|Contém informações sobre como executar trabalhos manualmente (sem uma agenda).|[Executar Trabalhos](../../ssms/agent/run-jobs.md)|  
|Contém informações sobre como configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para responder a trabalhos. Por exemplo, você pode configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para notificar administradores quando os trabalhos forem concluídos.|[Especificar respostas de trabalho](../../ssms/agent/specify-job-responses.md)|  
|Contém informações sobre como exibir trabalhos existentes, seu histórico quando executado, e como modificá-los.|[Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)|  
|Contém informações sobre como excluir trabalhos.|[excluir trabalhos](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>Consulte Também  
[Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
