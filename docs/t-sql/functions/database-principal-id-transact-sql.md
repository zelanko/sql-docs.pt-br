---
title: DATABASE_PRINCIPAL_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0fa5615d70542373030e0344d6988d9d2d0a028c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68026264"
---
# <a name="database_principal_id-transact-sql"></a>DATABASE_PRINCIPAL_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Essa função retorna o número de ID de uma entidade de segurança no banco de dados atual. Veja [Entidades de segurança &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md) para obter mais informações sobre entidades de segurança.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
*principal_name*  
É uma expressão do tipo **sysname** que representa a entidade de segurança. Quando *principal_name* é omitido, a `DATABASE_PRINCIPAL_ID` retorna a ID do usuário atual. `DATABASE_PRINCIPAL_ID` requer parênteses.
  
## <a name="return-types"></a>Tipos de retorno
**int**  
NULL quando a entidade de segurança do banco de dados não existe.
  
## <a name="remarks"></a>Comentários  
Use `DATABASE_PRINCIPAL_ID` em uma lista selecionada, uma cláusula WHERE ou qualquer lugar que permite que uma expressão. Para saber mais, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-id-of-the-current-user"></a>a. Recuperando a ID do usuário atual  
Este exemplo retorna a ID de entidade de segurança do banco de dados do usuário atual.
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### <a name="b-retrieving-the-id-of-a-specified-database-principal"></a>B. Recuperando a ID de uma entidade de segurança do banco de dados especificado  
Este exemplo retorna a ID de entidade de segurança do banco de dados para a função de banco de dados `db_owner`.
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## <a name="see-also"></a>Confira também
[Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  
