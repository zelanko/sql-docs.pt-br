---
title: sys.fn_hadr_is_primary_replica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_is_primary_replica
- fn_hadr_is_primary_replica_TSQL
- fn_hadr_is_primary_replica
- sys.fn_hadr_is_primary_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_hadr_is_primary_replica
- sys.fn_hadr_is_primary_replica
ms.assetid: c9b1969f-be1d-4dfb-a33d-551f380b9e27
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ebfd66acdc93f1a5148981e06f8adf1c507e1705
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240506"
---
# <a name="sysfnhadrisprimaryreplica-transact-sql"></a>sys.fn_hadr_is_primary_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Usado para determinar se a réplica atual for a réplica primária.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_hadr_is_primary_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*dbname*'  
 É o nome do banco de dados. *DBName* é do tipo sysname.  
  
## <a name="returns"></a>Retorna  
 Retornará 1 se o banco de dados na instância atual for a réplica primária. Caso contrário, retorna 0.  
  
## <a name="remarks"></a>Remarks  
 Use esta função para determinar se aparentemente a instância local está hospedando a réplica primária do banco de dados de disponibilidade especificado. O código de exemplo pode ser semelhante ao seguinte:  
  
```  
If sys.fn_hadr_is_primary_replica ( @dbname ) <> 1   
BEGIN  
-- If this is not the primary replica, exit (probably without error).  
END  
-- If this is the primary replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-sysfnhadrisprimaryreplica"></a>A. Usando sys.fn_hadr_is_primary_replica  
 O exemplo a seguir retornará 1 se o banco de dados especificado na instância local for a réplica primária.  
  
```  
SELECT sys.fn_hadr_is_primary_replica ('TestDB');  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Grupos de disponibilidade AlwaysOn & #40; SQL Server & #41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [CRIAR GRUPO de DISPONIBILIDADE &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [Exibições do catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)  
  
  
