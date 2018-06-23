---
title: Criar trabalhos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 40ec697eb5093ee690d944e0ec07cc01e2bf8ac6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008319"
---
# <a name="create-jobs"></a>Criar trabalhos
  Um trabalho é uma série especificada de operações executadas sequencialmente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Um trabalho pode realizar uma ampla gama de atividades, tais como a execução de scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , aplicativos de prompt de comando, scripts Microsoft ActiveX, pacotes do Integration Services, comandos e consultas do Analysis Services ou tarefas de replicação. Os trabalhos podem executar tarefas repetitivas ou agendáveis, bem como notificar usuários automaticamente sobre o status do trabalho, desse modo simplificando bastante a administração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para criar um trabalho, o usuário deve ser membro de uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou da função de servidor fixa **sysadmin** . Um trabalho só pode ser editado por seu proprietário ou por membros da função **sysadmin** . Os membros da função **sysadmin** podem atribuir a propriedade do trabalho a outros usuários, bem como executar qualquer trabalho, independentemente de seu proprietário. Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
 Podem ser criados trabalhos para execução na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em várias instâncias em toda a empresa. Para executar trabalhos em vários servidores, é necessário configurar pelo menos um servidor mestre e um ou mais servidores de destino. Para obter mais informações sobre servidores mestre e de destino, consulte [Administração automatizada em toda a empresa](automated-administration-across-an-enterprise.md)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent registra as informações do trabalho e suas etapas no histórico de trabalhos.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como criar um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Criar um trabalho](create-a-job.md)|  
|Descreve como reatribuir a propriedade de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a outro usuário.|[Give Others Ownership of a Job](give-others-ownership-of-a-job.md)|  
|Descreve como configurar o log de histórico de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Set Up the Job History Log](set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar etapas de trabalho](manage-job-steps.md)   
 [Administração automatizada em toda a empresa](automated-administration-across-an-enterprise.md)   
 [Criar e anexar agendas para trabalhos](create-and-attach-schedules-to-jobs.md)   
 [Executar trabalhos](run-jobs.md)   
 [Exibir ou modificar trabalhos](view-or-modify-jobs.md)  
  
  