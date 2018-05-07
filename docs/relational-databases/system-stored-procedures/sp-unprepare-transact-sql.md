---
title: sp_unprepare (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_unprepare_TSQL
- sp_cursor_unprepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unprepare
ms.assetid: 14320251-c551-49d8-b933-057406114978
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c444b5b8fbd83a490993dde2a864d60afa9b6932
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spunprepare-transact-sql"></a>sp_unprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Descarta o plano de execução criado pelo procedimento armazenado sp_prepare. sp_unprepare é invocado pela especificação de ID = 15 em um pacote de protocolo TDS de dados tabulares.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_unprepare handle           
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador*  
 É o *tratar* valor retornado por sp_prepare.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir prepara, executa e cancela a preparação de uma instrução simples.  
  
```  
Declare @P1 int;  
Exec sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
Exec sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir prepara, executa e cancela a preparação de uma instrução simples.  
  
```  
Declare @P1 int;  
Exec sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
Exec sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  

