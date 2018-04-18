---
title: sp_dbfixedrolepermission (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dbfixedrolepermission
- sp_dbfixedrolepermission_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbfixedrolepermission
ms.assetid: b8c30191-f532-49cd-83f3-c271f63ce572
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02ae10dc752b2122f2d7d86319b336bf5be3bc9f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spdbfixedrolepermission-transact-sql"></a>sp_dbfixedrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe as permissões de uma função de banco de dados fixa. **sp_dbfixedrolepermission** retorna informações corretas no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. A saída não reflete as alterações para a hierarquia de permissões que foram implementadas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, consulte[permissões &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbfixedrolepermission [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'***função***'**  
 É o nome de uma função de banco de dados fixa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *função* é **sysname**, com um padrão NULL. Se *função* não for especificado, as permissões para todas as funções fixas de banco de dados são exibidas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|Nome da função de banco de dados fixa|  
|**Permissão**|**nvarchar (70)**|Permissões associadas com **DbFixedRole**|  
  
## <a name="remarks"></a>Remarks  
 Para exibir uma lista das funções fixas de banco de dados, execute **sp_helpdbfixedrole**. A tabela a seguir mostra as funções de banco de dados fixas.  
  
|Função de banco de dados fixa|Description|  
|-------------------------|-----------------|  
|**db_owner**|Proprietários de banco de dados|  
|**db_accessadmin**|Administradores de acesso de banco de dados|  
|**db_securityadmin**|Administradores de segurança de banco de dados|  
|**db_ddladmin**|Administradores DDL (linguagem de definição de dados) de banco de dados|  
|**db_backupoperator**|Operadores de backup de banco de dados|  
|**db_datareader**|Leitores dos dados de banco de dados|  
|**db_datawriter**|Gravadores dos dados de banco de dados|  
|**db_denydatareader**|Leitores de negação dos dados de banco de dados|  
|**db_denydatawriter**|Gravadores de negação dos dados de banco de dados|  
  
 Membros de **db_owner** função fixa de banco de dados tem as permissões de todas as outras funções de banco de dados fixa. Para exibir as permissões para funções de servidor fixas, execute **sp_srvrolepermission**.  
  
 O conjunto de resultados inclui as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem ser executadas, e outras atividades especiais que podem ser realizadas, por membros da função de banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir retorna as permissões para todas as funções de banco de dados porque não especifica uma função de banco de dados fixa.  
  
```  
EXEC sp_dbfixedrolepermission;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helpdbfixedrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)   
 [sp_srvrolepermission &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
