---
title: DESCARTAR o POOL de recursos EXTERNOS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL RESOURCE POOL
- DROP_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs: TSQL
helpviewer_keywords: DROP EXTERNAL RESOURCE POOL statement
ms.assetid: e2fa01bd-96ff-4ea9-bb08-6cb6b6adf68c
caps.latest.revision: "6"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: edd6e956bc9453317c928a099469e65ddf5e0e0f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-external-resource-pool-transact-sql"></a>DESCARTAR o POOL de recursos EXTERNOS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Exclui um pool de recursos externos do administrador de recursos usado para definir recursos para processos externos. Para R Services controla o pool externo `rterm.exe`, `BxlServer.exe`e outros processos gerados por eles. Pools de recursos externos são criados usando [CREATE EXTERNAL RESOURCE POOL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-resource-pool-transact-sql.md) e modificados usando [ALTER EXTERNAL RESOURCE POOL &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-external-resource-pool-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome_do_pool*  
 O nome do pool de recursos externos a ser excluído.  
  
## <a name="remarks"></a>Comentários  
 Você não pode descartar um pool de recursos externos, se ele contiver grupos de carga de trabalho.  
  
 Você não pode descartar os pools internos ou padrão do Administrador de recursos.  
  
 A reconfiguração n  
  
 Ao executar instruções DDL, é recomendável estar familiarizado com os estados do Administrador de Recursos. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `CONTROL SERVER`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta o pool de recursos externos denominado `ex_pool`.  
  
```  
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Opção de configuração de servidor External scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Problemas conhecidos do SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTERAR o POOL de recursos EXTERNOS &#40; Transact-SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [Remover POOL de recursos &#40; Transact-SQL &#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)  
  
  
