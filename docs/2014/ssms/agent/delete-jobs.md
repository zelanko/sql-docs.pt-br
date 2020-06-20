---
title: Excluir trabalhos | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: stevestein
ms.author: sstein
ms.openlocfilehash: f66387a1334f91c29b8edddad293d76064430b39
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995465"
---
# <a name="delete-jobs"></a>excluir trabalhos
  Um trabalho é uma série especificada de operações executadas sequencialmente pelo SQL Server Agent. Por padrão, os trabalhos não são excluídos quando a execução termina. Você pode excluir um ou mais trabalhos do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent independentemente do êxito ou da falha do trabalho. Também é possível configurar o [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para excluir trabalhos automaticamente quando eles obtiverem êxito, falharem ou forem concluídos.  
  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar o sp_delete_job &#40;procedimento armazenado do sistema [&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql) para excluir um trabalho. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
 Membros da função de servidor fixa **sysadmin** podem executar **sp_delete_job** para excluir qualquer trabalho. Um usuário que não for membro da função de servidor fixa **sysadmin** poderá excluir somente os trabalhos que forem de sua propriedade.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como excluir um ou mais trabalhos do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Excluir um ou mais trabalhos](delete-one-or-more-jobs.md)|  
|Descreve como configurar o [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para excluir trabalhos automaticamente quando eles obtiverem êxito, falharem ou forem concluídos.|[Automatically Delete a Job](automatically-delete-a-job.md)|  
  
  
