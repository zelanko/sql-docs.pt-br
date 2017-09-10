---
title: IDENT_INCR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IDENT_INCR
- IDENT_INCR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- incremental values [SQL Server]
- IDENT_INCR function
- identity columns [SQL Server], IDENT_INCR function
ms.assetid: e13b491f-4f1f-4cb6-8b63-5084120f98cf
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dc4422adbc505a7ff6ac813c39e1567b249856c2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="identincr-transact-sql"></a>IDENT_INCR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o valor de incremento (retornado como **numérico** (**@@**MAXPRECISION,0)) especificado durante a criação de uma coluna identity em uma tabela ou exibição que tenha uma coluna de identidade.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IDENT_INCR ( 'table_or_view' )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *table_or_view* **'**  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) especificando a tabela ou exibição para verificar se há um valor de incremento de identidade válida. *table_or_view* pode ser uma constante de cadeia de caracteres entre aspas, uma variável, uma função ou um nome de coluna. *table_or_view* é **char**, **nchar**, **varchar**, ou **nvarchar**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **numeric**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário só pode exibir os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha permissão concedida. Isso significa que as funções internas emissoras de metadados, como IDENT_INCR, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-increment-value-for-a-specified-table"></a>A. Retornando o valor de incremento de uma tabela especificada  
 O exemplo a seguir retorna o valor de incremento para a tabela `Person.Address` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENT_INCR('Person.Address') AS Identity_Increment;  
GO  
```  
  
### <a name="b-returning-the-increment-value-from-multiple-tables"></a>B. Retornando o valor de incremento de várias tabelas  
 O exemplo a seguir retorna as tabelas no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] que incluem uma coluna de identidade com um valor de incremento.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_SCHEMA, TABLE_NAME,   
   IDENT_INCR(TABLE_SCHEMA + '.' + TABLE_NAME) AS IDENT_INCR  
FROM INFORMATION_SCHEMA.TABLES  
WHERE IDENT_INCR(TABLE_SCHEMA + '.' + TABLE_NAME) IS NOT NULL;  
```  
  
 Este é um conjunto de resultados parcial.  
  
 `TABLE_SCHEMA        TABLE_NAME                IDENT_INCR`  
  
 `------------        ------------------------  ----------`  
  
 `Person              Address                            1`  
  
 `Production          ProductReview                      1`  
  
 `Production          TransactionHistory                 1`  
  
 `Person              AddressType                        1`  
  
 `Production          ProductSubcategory                 1`  
  
 `Person              vAdditionalContactInfo             1`  
  
 `dbo                 AWBuildVersion                     1`  
  
 `Production          BillOfMaterials                    1`  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENT_SEED &#40; Transact-SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [. identity_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  
