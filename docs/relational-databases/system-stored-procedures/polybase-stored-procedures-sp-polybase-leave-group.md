---
title: sp_polybase_leave_group (Transact-SQL) | Microsoft Docs
description: O comando Transact-SQL sp_polybase_leave_group remove uma instância de SQL Server de um grupo polybase para cálculo de expansão.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3d909da06b0f8cf4520d92a9ba8cb8652a6b2a5a
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753880"
---
# <a name="sp_polybase_leave_group-transact-sql"></a>sp_polybase_leave_group (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Remove uma instância de SQL Server de um grupo polybase para cálculo de expansão. 
 
 A instância de SQL Server deve ter o recurso de  [Guia do polybase](../../relational-databases/polybase/polybase-guide.md) instalado.  O polybase permite a integração de fontes de dados não SQL Server, como o Hadoop e o armazenamento de BLOBs do Azure. Consulte também [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="remarks"></a>Comentários  
 Você só pode remover um nó de computação de um grupo.  
  
 Depois de executar o procedimento armazenado, reinicie o mecanismo do polybase e o serviço de Movimentação de Dados PolyBase no computador. Para verificar, execute o seguinte DMV no nó principal: **Sys.dm_exec_compute_nodes**.  
  
## <a name="example"></a>Exemplo  
 O exemplo remove a máquina atual de um grupo do polybase.  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Introdução ao PolyBase](../polybase/polybase-guide.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
