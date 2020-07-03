---
title: sp_delete_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobschedule
- sp_delete_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobschedule
ms.assetid: 82fbb48b-603a-4016-a7fb-1ce17fb76919
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8a74d7235b1faa80c1fe65f80717c39e7944f343
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85864268"
---
# <a name="sp_delete_jobschedule-transact-sql"></a>sp_delete_jobschedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exclui uma agenda para um trabalho.  
  
 **sp_delete_jobschedule** é fornecido somente para fins de compatibilidade com versões anteriores.  
  
  
## <a name="remarks"></a>Comentários  
 As agendas de trabalho podem ser gerenciadas independentemente dos trabalhos. Para remover uma agenda de um trabalho, use **sp_detach_schedule**. Para excluir uma agenda, use **sp_delete_schedule**.  
  
> **Observação: sp_delete_jobschedule** não dá suporte a agendas que estão anexadas a vários trabalhos. Se um script existente chamar **sp_delete_jobschedule** para remover uma agenda anexada a mais de um trabalho, o procedimento retornará um erro.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros da função **sysadmin** podem excluir qualquer agendamento de trabalho. Os usuários que não são membros da função **sysadmin** só podem excluir agendas de trabalho de sua propriedade.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_delete_schedule](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_detach_schedule](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)   
 [&#41;&#40;Transact-SQL de sp_add_schedule](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_jobschedule](../../relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_jobschedule](../../relational-databases/system-stored-procedures/sp-update-jobschedule-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
