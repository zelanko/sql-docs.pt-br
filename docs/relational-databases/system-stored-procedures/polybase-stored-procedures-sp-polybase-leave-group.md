---
title: sp_polybase_leave_group (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
caps.latest.revision: 11
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8ad3a202ff910d19ea70192eb9cc5e114a8a4cb9
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="sppolybaseleavegroup-transact-sql"></a>sp_polybase_leave_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Remove uma instância do SQL Server de um grupo de PolyBase para a computação de expansão. 
 
 A instância do SQL Server deve ter o [guia do PolyBase](../../relational-databases/polybase/polybase-guide.md) recurso instalado.  O PolyBase permite a integração de fontes de dados do SQL Server, como o armazenamento de blob de Hadoop e o Azure. Consulte também [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="remarks"></a>Remarks  
 Você só pode remover um nó de computação de um grupo.  
  
 Depois de executar o procedimento armazenado, reinicie o mecanismo de PolyBase e o serviço de movimentação de dados de PolyBase na máquina. Para verificar a executar a seguinte DMV no nó principal: **sys.DM exec_compute_nodes**.  
  
## <a name="example"></a>Exemplo  
 O exemplo remove o computador atual de um grupo de PolyBase.  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
