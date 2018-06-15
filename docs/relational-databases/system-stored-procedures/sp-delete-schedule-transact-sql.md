---
title: sp_delete_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_schedule
- sp_delete_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_schedule
ms.assetid: 18b2c985-47b8-49c8-82d1-8a4af3d7d33a
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14fd520f5447092e5f82dc786696148f3dbe3bd3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33255940"
---
# <a name="spdeleteschedule-transact-sql"></a>sp_delete_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui uma agenda.  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_schedule { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @force_delete = ] force_delete  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@schedule_id=** ] *schedule_id*  
 O número de identificação da agenda a ser excluída. *schedule_id* é **int**, com um padrão NULL.  
  
> **Observação:** ou *schedule_id* ou *schedule_name* devem ser especificados, mas não é possível especificar ambos.  
  
 [  **@schedule_name=** ] **'***schedule_name***'**  
 O nome da agenda a ser excluída. *schedule_name* é **sysname**, com um padrão NULL.  
  
> **Observação:** ou *schedule_id* ou *schedule_name* devem ser especificados, mas não é possível especificar ambos.  
  
 [ **@force_delete** =] *force_delete*  
 Especifica se o procedimento deve falhar se a agenda estiver anexada a um trabalho. *Force_delete* é bit, com um padrão de **0**. Quando *force_delete* é **0**, o procedimento armazenado falhará se a agenda estiver anexada a um trabalho. Quando *force_delete* é **1**, a agenda será excluída, independentemente se a agenda estiver anexada a um trabalho.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Por padrão, uma agenda não poderá ser excluída se estiver anexada a um trabalho. Para excluir uma agenda que é anexada a um trabalho, especifique um valor de **1** para *force_delete*. A exclusão de uma agenda não para trabalhos que estejam atualmente em execução.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Observe que o proprietário do trabalho pode anexar e desanexar o trabalho de uma agenda sem precisar ser também o proprietário da agenda. No entanto, uma agenda não pode ser excluída se a desanexação deixá-la sem trabalhos, a menos que o chamador seja o proprietário da agenda.  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Somente membros do **sysadmin** função pode excluir uma agenda de trabalho que pertence a outro usuário.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-deleting-a-schedule"></a>A. Excluindo uma agenda  
 O exemplo a seguir exclui a agenda `NightlyJobs`. Se a agenda estiver anexada a qualquer trabalho, o exemplo não excluirá a agenda.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="b-deleting-a-schedule-attached-to-a-job"></a>B. Excluindo uma agenda anexada a um trabalho  
 O exemplo a seguir exclui a agenda `RunOnce`, independentemente do fato de a agenda estar anexada a um trabalho.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = 'RunOnce',  
    @force_delete = 1;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Implementar trabalhos](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
  
