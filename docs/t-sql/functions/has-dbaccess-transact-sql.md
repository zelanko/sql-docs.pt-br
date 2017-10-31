---
title: HAS_DBACCESS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAS_DBACCESS_TSQL
- HAS_DBACCESS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- permissions [SQL Server], user access status
- HAS_DBACCESS
- checking permission status
- verifying permission status
- users [SQL Server], access rights status
- testing permissions
- status information [SQL Server], user access
ms.assetid: 99b43a72-0722-4a7b-a493-bdee1c74c7b9
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: efb5681a5ca390fb2c00033dbbfc70c27ae9544e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="hasdbaccess-transact-sql"></a>HAS_DBACCESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Retorna informações que indicam se o usuário tem acesso ao banco de dados especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HAS_DBACCESS ( 'database_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*database_name*'  
 O nome do banco de dados para o qual o usuário deseja informações de acesso. *Database_Name* é **sysname**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 HAS_DBACCESS retornará 1 se o usuário tiver acesso ao banco de dados, 0 se o usuário não tiver acesso ao banco de dados e NULL se o nome do banco de dados não for válido.  
  
 HAS_DBACCESS retornará 0 se o banco de dados estiver offline e for suspeito.  
  
 HAS_DBACCESS retornará 0 se o banco de dados estiver no modo de usuário único e se o banco de dados estiver sendo usado por outro usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir testa se o usuário atual tem acesso ao banco de dados `AdventureWorks2012`.  
  
```  
SELECT HAS_DBACCESS('AdventureWorks2012');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir testa se o usuário atual tem acesso ao banco de dados `AdventureWorksPDW2012`.  
  
```  
SELECT HAS_DBACCESS('AdventureWorksPDW2012');  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)  
  
  


