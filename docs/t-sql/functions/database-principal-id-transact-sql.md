---
title: DATABASE_PRINCIPAL_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_PRINCIPAL_ID_TSQL
- DATABASE_PRINCIPAL_ID
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], principals
- principal ID numbers [SQL Server]
- DATABASE_PRINCIPAL_ID function
- IDs [SQL Server], principals
ms.assetid: 908c7dd8-c10b-4658-92f6-0224f9835dd9
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a26dcac49e19f9a0dda738e58042c83cb8e46b8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="databaseprincipalid-transact-sql"></a>DATABASE_PRINCIPAL_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o número de ID de um principal no banco de dados atual. Para obter mais informações sobre entidades de segurança, consulte [entidades &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
*principal_name*  
É uma expressão do tipo **sysname** que representa a entidade de segurança.  
Quando *principal_name* é omitido, a ID do usuário atual será retornada. Os parênteses são necessários.
  
## <a name="return-types"></a>Tipos de retorno
**int**  
NULL quando a entidade de banco de dados não existe
  
## <a name="remarks"></a>Comentários  
DATABASE_PRINCIPAL_ID pode ser usado em uma lista de seleção, cláusula WHERE ou em qualquer local em que uma expressão for permitida. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-id-of-the-current-user"></a>A. Recuperando a ID do usuário atual  
O exemplo a seguir retorna a ID de principal do banco de dados do usuário atual.
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### <a name="b-retrieving-the-id-of-a-specified-database-principal"></a>B. Recuperando a ID de uma entidade de segurança do banco de dados especificado  
O exemplo a seguir retorna a ID de principal do banco de dados para a função de banco de dados `db_owner`.
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  

