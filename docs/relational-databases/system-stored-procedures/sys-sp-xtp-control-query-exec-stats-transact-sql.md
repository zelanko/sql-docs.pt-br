---
title: sys. sp_xtp_control_query_exec_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_query_exec_stats_TSQL
- sys.sp_xtp_control_query_exec_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_query_exec_stats
ms.assetid: 4838125d-ad1e-479e-b7d2-42655e8f4f02
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd8ee38dc4ac1a8fd3a729d94744d3fd98f78875
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017853"
---
# <a name="syssp_xtp_control_query_exec_stats-transact-sql"></a>sys.sp_xtp_control_query_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Habilita a coleta de estatísticas por consulta para todos os procedimentos armazenados compilados nativamente para a instância ou para procedimentos armazenados compilados nativamente específicos.  
  
 Reduz o desempenho quando você habilita a coleta de estatísticas. Se você precisar solucionar problemas de um ou alguns procedimentos armazenados compilados nativamente, será necessário habilitar a coleta de estatísticas apenas para esses.  
  
 Para habilitar a coleta de estatísticas no nível de procedimento para todos os procedimentos armazenados compilados nativamente, consulte [Sys. sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_xtp_control_query_exec_stats [ [ @new_collection_value = ] collection_value ],  
[ [ @database_id = ] database_id   
[ , [ @xtp_object_id = ] procedure_id ] ,   
[ @old_collection_value] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 @new_collection_value= *valor*  
 Determina se a coleta de estatísticas no nível do procedimento está ativada (1) ou desativada (0).  
  
 @new_collection_valueé definido como zero quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado.  
  
 @database_id= = *database_id*, @xtp_object_id = *procedure_id*  
 A ID de banco de dados e a ID de objeto do procedimento armazenado compilado nativamente. Se a coleta de estatísticas estiver habilitada para a instância ([Sys. sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md)), as estatísticas em um procedimento armazenado compilado nativamente serão coletadas. Se você desativar a coleção de estatísticas na instância, ela não será desativada para cada procedimento armazenado compilado de forma nativa.  
  
 Use [Sys. databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md), [sys. procedimentos &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md), [DB_ID &#40;transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)ou [object_id &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md) para obter IDs para um banco de dados e um procedimento armazenado.  
  
 @old_collection_value= *valor*  
 Retorna o status atual.  
  
## <a name="return-code"></a>Código de retorno  
 0 para êxito. Diferente de zero para falha.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função sysadmin fixa.  
  
## <a name="code-sample"></a>Exemplo de código  
 O exemplo de código a seguir mostra como habilitar a coleta de estatísticas para todos os procedimentos armazenados compilados nativamente para a instância e, depois, para um procedimento armazenado compilado nativamente específico.  
  
```sql   
DECLARE @c bit  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1;  
  
EXEC sp_xtp_control_query_exec_stats @old_collection_value=@c output;  
SELECT @c AS 'collection status';  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
@database_id = 5, @xtp_object_id = 341576255;  
  
EXEC sp_xtp_control_query_exec_stats @database_id = 5,   
@xtp_object_id = 341576255, @old_collection_value=@c output;  
  
SELECT @c AS 'collection status';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
