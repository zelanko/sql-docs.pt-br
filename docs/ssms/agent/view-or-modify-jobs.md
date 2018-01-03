---
title: Exibir ou modificar trabalhos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d006a04846dfca3005cf0ecb40737e31c974e07
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="view-or-modify-jobs"></a>Exibir ou modificar trabalhos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Você pode exibir qualquer trabalho que tenha criado. Após executar um trabalho, você também pode exibir seu histórico. Exibir o histórico de um trabalho permite-lhe observar quando o trabalho foi executado, o status do trabalho como um todo e o status de cada etapa do trabalho. É possível saber se o trabalho já falhou no passado, quando foi concluído com êxito pela última vez e que saída o trabalho criou a cada execução. Os membros da função de servidor fixa **sysadmin** podem exibir ou modificar qualquer trabalho, independentemente do proprietário.  
  
> [!NOTE]  
> Um trabalho deve ter sido executado pelo menos uma vez para haver um histórico de trabalhos. Você pode limitar o tamanho total do log de histórico do trabalho, bem com o tamanho por trabalho.  
  
Além disso, você também pode modificar um trabalho para atender a novos requisitos. É possível modificar:  
  
-   Opções de resposta  
  
-   Agendamentos  
  
-   Etapas de trabalho  
  
-   Propriedade  
  
-   Categoria do trabalho  
  
-   Servidores de destino (somente em trabalhos multisservidor)  
  
Para assegurar que as alterações em trabalhos multisservidor entrem em vigor, é necessário postá-las na lista de downloads para que os servidores de destino possam baixar o trabalho atualizado. Para garantir que os servidores de destino disponham das definições de trabalho mais atuais, poste uma instrução INSERT após atualizar o trabalho multisservidor, da seguinte maneira:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Para obter mais informações, consulte [sp_purge_jobhistory (Transact-SQL)](http://msdn.microsoft.com/en-us/237f9bad-636d-4262-9bfb-66c034a43e88).  
  
Os membros da função de servidor fixa **sysadmin** podem exibir a definição ou o histórico de qualquer trabalho, bem como modificá-los.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como exibir trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[View a Job](../../ssms/agent/view-a-job.md)|  
|Descreve como exibir o log de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[View the Job History](../../ssms/agent/view-the-job-history.md)|  
|Descreve como excluir o conteúdo do log de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Clear the Job History Log](../../ssms/agent/clear-the-job-history-log.md)|  
|Descreve como definir limites de tamanho para logs de históricos de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Resize the Job History Log](../../ssms/agent/resize-the-job-history-log.md)|  
|Descreve como alterar as propriedades de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Modify a Job](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>Consulte Também  
[sysjobhistory](http://msdn.microsoft.com/en-us/1b1fcdbb-2af2-45e6-bf3f-e8279432ce13)  
  
