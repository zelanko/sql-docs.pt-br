---
title: Excluir trabalhos | Microsoft Docs
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
helpviewer_keywords: delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be3069cfd5be3845c6c3f2f08b9a17bb7243ee4e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="delete-jobs"></a>excluir trabalhos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Um trabalho é uma série especificada de operações executadas sequencialmente pelo SQL Server Agent. Por padrão, os trabalhos não são excluídos quando a execução termina. Você pode excluir um ou mais trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent independentemente do êxito ou da falha do trabalho. Também é possível configurar o [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para excluir trabalhos automaticamente quando eles obtiverem êxito, falharem ou forem concluídos.  
  
Por padrão, os membros da função de servidor fixa **sysadmin** podem executar o procedimento armazenado do sistema [sp_delete_job (Transact-SQL)](http://msdn.microsoft.com/en-us/b85db6e4-623c-41f1-9643-07e5ea38db09) para excluir um trabalho. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Membros da função de servidor fixa **sysadmin** podem executar **sp_delete_job** para excluir qualquer trabalho. Um usuário que não for membro da função de servidor fixa **sysadmin** poderá excluir somente os trabalhos que forem de sua propriedade.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como excluir um ou mais trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.|[Excluir um ou mais trabalhos](../../ssms/agent/delete-one-or-more-jobs.md)|  
|Descreve como configurar o [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para excluir trabalhos automaticamente quando eles obtiverem êxito, falharem ou forem concluídos.|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
  
