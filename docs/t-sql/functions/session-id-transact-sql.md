---
title: SESSION_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2a0d500a-f6c8-490f-9abd-3ae824986404
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9089c21109d6eedb1cdae0082e1530e8d77d9dde
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna a ID da atual [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] sessão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **nvarchar (32)** valor.  
  
## <a name="general-remarks"></a>Comentários gerais  
 A ID de sessão é atribuída a cada conexão de usuário quando a conexão é feita. Persistir durante a conexão. Quando termina a conexão, a ID de sessão é liberada.  
  
 A ID de sessão começa com os caracteres alfabéticos 'SID'. Essas diferenciam maiusculas de minúsculas e deve estar em letras maiusculas quando a ID de sessão é usada em [!INCLUDE[DWsql](../../includes/dwsql-md.md)] comandos.  
  
 Você pode consultar a exibição [sys.dm_pdw_exec_sessions](http://msdn.microsoft.com/en-us/5b656c55-427f-4306-8bd9-9d7987c203d9) para recuperar as mesmas informações que essa função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a ID da sessão atual.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>Consulte também  
 [DB_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSÃO do &#40; SQL Data Warehouse &#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  

