---
title: SESSION_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 117e5a08730aae4381f10fc8a8a2ab0ed2fa875f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65945227"
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
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor de **nvarchar(32)** .  
  
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
  
  
