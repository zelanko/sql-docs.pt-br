---
title: Exibir ou modificar trabalhos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9ddbf1591320678c75f74d6953229343bb457ced
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "42775460"
---
# <a name="view-or-modify-jobs"></a>Exibir ou modificar trabalhos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Você pode exibir qualquer trabalho criado. Após executar um trabalho, você também pode exibir seu histórico. Exibir o histórico de um trabalho permite-lhe observar quando o trabalho foi executado, o status do trabalho como um todo e o status de cada etapa do trabalho. É possível saber se o trabalho já falhou no passado, quando foi concluído com êxito pela última vez e que saída o trabalho criou a cada execução. Os membros da função de servidor fixa **sysadmin** podem exibir ou modificar qualquer trabalho, independentemente do proprietário.  
  
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
  
Para obter mais informações, consulte [sp_purge_jobhistory (Transact-SQL)](http://msdn.microsoft.com/237f9bad-636d-4262-9bfb-66c034a43e88).  
  
Os membros da função de servidor fixa **sysadmin** podem exibir a definição ou o histórico de qualquer trabalho, bem como modificá-los.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como exibir trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[View a Job](../../ssms/agent/view-a-job.md)|  
|Descreve como exibir o log de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[View the Job History](../../ssms/agent/view-the-job-history.md)|  
|Descreve como excluir o conteúdo do log de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Clear the Job History Log](../../ssms/agent/clear-the-job-history-log.md)|  
|Descreve como definir limites de tamanho para logs de históricos de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Resize the Job History Log](../../ssms/agent/resize-the-job-history-log.md)|  
|Descreve como alterar as propriedades de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Modify a Job](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>Consulte Também  
[sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
