---
title: TYPE_NAME (Transact-SQL) | Microsoft Docs
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
- TYPE_NAME_TSQL
- TYPE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- names [SQL Server], data types
- unqualified type names
- type names [SQL Server]
- data types [SQL Server], names
- TYPE_NAME function
ms.assetid: e4075a2e-5f70-440f-986b-9ec8434e07c1
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3d60bec3a21bb5b1127b0f18977d3485979f20b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="typename-transact-sql"></a>TYPE_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o nome de tipo não qualificado de um ID de tipo especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TYPE_NAME ( type_id )   
```  
  
## <a name="arguments"></a>Argumentos  
 *type_id*  
 É a ID do tipo que será usado. *type_id* é um **int**, e pode se referir a um tipo em qualquer esquema que o chamador tenha permissão para acessar.  
  
## <a name="return-types"></a>Tipos de retorno  
 **sysname**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário só pode exibir os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha permissão concedida. Isso significa que funções internas que emitem metadados, como TYPE_NAME, poderão retornar o NULL se o usuário não tiver nenhuma permissão para o objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentários  
 TYPE_NAME retorna NULL quando *type_id* não é válido ou quando o chamador não tem permissão suficiente para o tipo de referência.  
  
 TYPE_NAME funciona para tipos de dados de sistema e também para tipos de dados definidos pelo usuário. O tipo pode estar contido em qualquer esquema, mas um nome de tipo não qualificado sempre será retornado. Isso significa que o nome não tem o *esquema***.** prefixo.  
  
 As funções de sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local onde uma expressão for permitida. Para obter mais informações, consulte [expressões &#40; Transact-SQL &#41; ](../../t-sql/language-elements/expressions-transact-sql.md) e [onde &#40; Transact-SQL &#41; ](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o nome de objeto, nome de coluna e nome de tipo para cada coluna na tabela `Vendor` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
SELECT o.name AS obj_name, c.name AS col_name,  
       TYPE_NAME(c.user_type_id) AS type_name  
FROM sys.objects AS o   
JOIN sys.columns AS c  ON o.object_id = c.object_id  
WHERE o.name = 'Vendor'  
ORDER BY col_name;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `obj_name        col_name                  type_name`  
  
 `--------------- ------------------------ --------------`  
  
 `Vendor          AccountNumber            AccountNumber`  
  
 `Vendor          ActiveFlag               Flag`  
  
 `Vendor          BusinessEntityID         int`  
  
 `Vendor          CreditRating             tinyint`  
  
 `Vendor          ModifiedDate             datetime`  
  
 `Vendor          Name                     Name`  
  
 `Vendor          PreferredVendorStatus    Flag`  
  
 `Vendor          PurchasingWebServiceURL  nvarchar`  
  
 `(8 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna o `TYPE ID` para o tipo de dados com a id `1`.  
  
```  
SELECT TYPE_NAME(36) AS Type36, TYPE_NAME(239) AS Type239;  
GO  
```  
  
 Para obter uma lista de tipos de consulta Types.  
  
```  
SELECT * FROM sys.types;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [TYPE_ID &#40; Transact-SQL &#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
  
  


