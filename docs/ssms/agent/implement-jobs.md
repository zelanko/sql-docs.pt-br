---
title: Implementar Trabalhos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27c654a36d652abe632fb7e2063760893ec6b06e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="implement-jobs"></a>Implementar trabalhos
É possível usar trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para automatizar tarefas administrativas de rotina e executá-las recorrentemente, tornando a administração mais eficaz.  
  
Um trabalho é uma série especificada de operações executadas sequencialmente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Um trabalho pode realizar uma ampla gama de atividades, tais como a execução de scripts [!INCLUDE[tsql](../../includes/tsql_md.md)] , aplicativos de linha de comando, scripts Microsoft ActiveX, pacotes do Integration Services, comandos e consultas do Analysis Services ou tarefas de replicação. Os trabalhos podem executar tarefas repetitivas ou agendáveis, bem como notificar usuários automaticamente sobre o status do trabalho por meio de alertas, desse modo simplificando bastante a administração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
É possível executar um trabalho manualmente ou configurá-lo para executar de acordo com uma agenda ou em resposta a alertas.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|||  
|-|-|  
|**Description**|**Tópico**|  
|Contém informações sobre como criar trabalhos e atribuir propriedade.|[Criar trabalhos](../../ssms/agent/create-jobs.md)|  
|Contém informações sobre como organizar trabalhos em categorias.|[Organizar trabalhos](../../ssms/agent/organize-jobs.md)|  
|Contém informações sobre os diferentes tipos de etapas de trabalho que podem ser criadas e como gerenciá-las.|[Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)|  
|Contém informações sobre como definir o início e a frequência da execução de trabalhos.|[Criar e anexar agendas para trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|Contém informações sobre como executar trabalhos manualmente (sem uma agenda).|[Executar Trabalhos](../../ssms/agent/run-jobs.md)|  
|Contém informações sobre como configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para responder a trabalhos. Por exemplo, você pode configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para notificar administradores quando os trabalhos forem concluídos.|[Especificar respostas de trabalho](../../ssms/agent/specify-job-responses.md)|  
|Contém informações sobre como exibir trabalhos existentes, seu histórico quando executado, e como modificá-los.|[Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)|  
|Contém informações sobre como excluir trabalhos.|[Excluir trabalhos](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>Consulte também  
[Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
