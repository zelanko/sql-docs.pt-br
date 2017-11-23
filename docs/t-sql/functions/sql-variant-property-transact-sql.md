---
title: SQL_VARIANT_PROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQL_VARIANT_PROPERTY_TSQL
- SQL_VARIANT_PROPERTY
dev_langs: TSQL
helpviewer_keywords:
- SQL_VARIANT_PROPERTY function
- sql_variant data type
ms.assetid: 50e5c1d9-4e95-4ed0-9c92-435c872a399e
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5947528f4e8959de1b8b4ee3679d4e3e058476d5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sqlvariantproperty-transact-sql"></a>SQL_VARIANT_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o tipo de base de dados e outras informações sobre um **sql_variant** valor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É uma expressão do tipo **sql_variant**.  
  
 *propriedade*  
 Contém o nome do **sql_variant** propriedade para a qual informações deverá ser fornecido. *propriedade* é **varchar (**128**)**, e pode ser qualquer um dos seguintes valores:  
  
|Valor|Description|Tipo base de sql_variant retornado|  
|-----------|-----------------|----------------------------------------|  
|**BaseType**|Tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como:<br /><br /> **bigint**<br /><br /> **binary**<br /><br /> **char**<br /><br /> **date**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **int**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **smallint**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = A entrada não é válida.|  
|**Precisão**|Número de dígitos do tipo de dados base numérico:<br /><br /> **DateTime** = 23<br /><br /> **smalldatetime** = 16<br /><br /> **float** = 53<br /><br /> **real** = 24<br /><br /> **decimal** (p, s) e **numérico** (p, s) = p<br /><br /> **Money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **bit** = 1<br /><br /> Todos os outros tipos = 0|**int**<br /><br /> NULL = A entrada não é válida.|  
|**Escala**|Número de dígitos à direita do ponto decimal do tipo de dados base numérico:<br /><br /> **decimal** (p, s) e **numérico** (p, s) = s<br /><br /> **Money** e **smallmoney** = 4<br /><br /> **DateTime** = 3<br /><br /> todos os outros tipos = 0|**int**<br /><br /> NULL = A entrada não é válida.|  
|**TotalBytes**|Número de bytes necessários para manter os metadados e os dados do valor. Essas informações seriam úteis na verificação do tamanho máximo de dados em um **sql_variant** coluna. Se o valor for maior que 900, a criação do índice falhará.|**int**<br /><br /> NULL = A entrada não é válida.|  
|**Agrupamento**|Representa o agrupamento de determinado **sql_variant** valor.|**sysname**<br /><br /> NULL = A entrada não é válida.|  
|**MaxLength**|Comprimento máximo do tipo de dados, em bytes. Por exemplo, **MaxLength** de **nvarchar (**50**)** é 100, **MaxLength** de **int** é 4.|**int**<br /><br /> NULL = A entrada não é válida.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **sql_variant**  
  
## <a name="examples"></a>Exemplos  
### <a name="a-using-a-sqlvariant-in-a-table"></a>A. Usando um sql_variant em uma tabela  
 O exemplo a seguir recupera `SQL_VARIANT_PROPERTY` informações sobre o `colA` valor `46279.1` onde `colB`  = `1689`, considerando que `tableA` tem `colA` que é do tipo `sql_variant` e `colB`.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]Observe que cada um destes três valores é uma **sql_variant**.  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. Usando um sql_variant como uma variável   
 O exemplo a seguir recupera `SQL_VARIANT_PROPERTY` informações sobre uma variável chamada @v1.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>Consulte também  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  

