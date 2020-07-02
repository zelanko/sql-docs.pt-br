---
title: sp_delete_maintenance_plan_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_maintenance_plan_db_TSQL
- sp_delete_maintenance_plan_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan_db
- maintenance plans [SQL Server], deleting
- removing maintenance plan
- disassociating maintenance plan
ms.assetid: d1e8afb5-12ee-492b-a770-ba708ed7c8a4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2935ecccb9ce0421396d552787d38b0b80fb3c45
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772232"
---
# <a name="sp_delete_maintenance_plan_db-transact-sql"></a>sp_delete_maintenance_plan_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Dissocia o plano de manutenção especificado do banco de dados especificado.  
  
> [!NOTE]  
>  Este procedimento armazenado é usado com planos de manutenção de banco de dados. Este recurso foi substituído por planos de manutenção que não usam esse procedimento armazenado. Use esse procedimento para manter planos de manutenção de banco de dados em instalações que foram atualizadas de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_maintenance_plan_db [ @plan_id = ] 'plan_id' ,   
     [ @db_name = ] 'database_name'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @plan_id = ] 'plan\_id'`Especifica a ID do plano de manutenção. *plan_id* é **uniqueidentifier**.  
  
`[ @db_name = ] 'database\_name'`Especifica o nome do banco de dados a ser excluído do plano de manutenção. *database_name* é **sysname**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_delete_maintenance_plan_db** deve ser executado do banco de dados **msdb** .  
  
 O procedimento armazenado **sp_delete_maintenance_plan_db** remove a associação entre o plano de manutenção e o banco de dados especificado; Ele não remove nem destrói o banco de dados.  
  
 Quando **sp_delete_maintenance_plan_db** remove o último banco de dados do plano de manutenção, o procedimento armazenado também exclui o plano de manutenção.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_delete_maintenance_plan_db**.  
  
## <a name="examples"></a>Exemplos  
 Exclui o plano de manutenção no banco de dados **AdventureWorks2012** , adicionado anteriormente usando **sp_add_maintenance_plan_db**.  
  
```  
EXECUTE   sp_delete_maintenance_plan_db N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Procedimentos armazenados do plano de manutenção de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
