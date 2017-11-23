---
title: DESCARTAR a CREDENCIAL de escopo do banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE SCOPED CREDENTIAL
- DROP_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- DROP DATABASE SCOPED CREDENTIAL statement
- credential [SQL Server], DROP DATABASE SCOPED CREDENTIAL statement
ms.assetid: 319d59f4-fa82-47ca-869b-3a9cd52900b0
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60271a08e7a48e60153b1e556c61e44a9a2c48a8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-database-scoped-credential-transact-sql"></a>DESCARTAR a CREDENCIAL de escopo do banco de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Remove uma credencial no escopo do banco de dados do servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP DATABASE SCOPED CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 É o nome da credencial no escopo do banco de dados para remover o servidor.  
  
## <a name="remarks"></a>Comentários  
 Para descartar o segredo associado a uma credencial no escopo do banco de dados sem descartar a credencial no escopo do banco de dados em si, use [ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md).  
  
 Informações sobre credenciais no escopo do banco de dados são visíveis no [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Requer `ALTER` permissão na credencial.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a credencial no escopo do banco de dados chamada `SalesAccess`.  
  
```tsql  
DROP DATABASE SCOPED CREDENTIAL AppCred;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Credenciais &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
