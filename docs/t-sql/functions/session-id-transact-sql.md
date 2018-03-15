---
title: SESSION_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/23/2018
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fbc453282e442e9adb5a378c216b2e5a83eb2bb0
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/24/2018
---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna a ID da sessão de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor de **nvarchar(32)**.  
  
## <a name="general-remarks"></a>Comentários gerais  
 A ID de sessão é atribuída a cada conexão de usuário quando esta é estabelecida. Ela é persistente durante a conexão. Quando a conexão é encerrada, a ID de sessão é liberada.  
  
 A ID de sessão começa com os caracteres alfabéticos 'SID'. Eles diferenciam maiúsculas de minúsculas e devem estar em maiúsculas quando a ID de sessão é usada em comandos [!INCLUDE[DWsql](../../includes/dwsql-md.md)].  
  
 Consulte a exibição [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para recuperar as mesmas informações que essa função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a ID da sessão atual.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40;SQL Data Warehouse&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
