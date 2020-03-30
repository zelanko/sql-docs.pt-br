---
title: SQL_VARIANT_PROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_VARIANT_PROPERTY_TSQL
- SQL_VARIANT_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- SQL_VARIANT_PROPERTY function
- sql_variant data type
ms.assetid: 50e5c1d9-4e95-4ed0-9c92-435c872a399e
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 22b11ff1f9a6ed218b4c63c2f22bfb6e2d441703
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74550193"
---
# <a name="sql_variant_property-transact-sql"></a>SQL_VARIANT_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o tipo de dados base e outras informações sobre um valor **sql_variant**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É uma expressão do tipo **sql_variant**.  
  
 *property*  
 Contém o nome da propriedade **sql_variant** cujas informações devem ser fornecidas. *property* é **varchar(** 128 **)** e pode ser um dos seguintes valores:  
  
|Valor|DESCRIÇÃO|Tipo base de sql_variant retornado|  
|-----------|-----------------|----------------------------------------|  
|**BaseType**|Tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como:<br /><br /> **bigint**<br /><br /> **binary**<br /><br /> **char**<br /><br /> **date**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **int**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **smallint**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = A entrada não é válida.|  
|**Precisão**|Número de dígitos do tipo de dados base numérico:<br /><br /> **datetime** = 23<br /><br />**datetime2** = 27<br /><br /> **smalldatetime** = 16<br /><br /> **float** = 53<br /><br /> **real** = 24<br /><br /> **decimal** (p,s) e **numeric** (p,s) = p<br /><br /> **money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **bit** = 1<br /><br /> Todos os outros tipos = 0|**int**<br /><br /> NULL = A entrada não é válida.|  
|**Escala**|Número de dígitos à direita do ponto decimal do tipo de dados base numérico:<br /><br /> **decimal** (p,s) e **numeric** (p,s) = s<br /><br /> **money** e **smallmoney** = 4<br /><br /> **datetime** = 3<br /><br />**datetime2** = 7<br /><br /> todos os outros tipos = 0|**int**<br /><br /> NULL = A entrada não é válida.|  
|**TotalBytes**|Número de bytes necessários para manter os metadados e os dados do valor. Essas informações serão úteis na verificação do tamanho máximo dos dados em uma coluna **sql_variant**. Se o valor for maior que 900, a criação do índice falhará.|**int**<br /><br /> NULL = A entrada não é válida.|  
|**Ordenação**|Representa a ordenação do valor **sql_variant** específico.|**sysname**<br /><br /> NULL = A entrada não é válida.|  
|**MaxLength**|Comprimento máximo do tipo de dados, em bytes. Por exemplo, **MaxLength** de **nvarchar(** 50 **)** é 100 e **MaxLength** de **int** é 4.|**int**<br /><br /> NULL = A entrada não é válida.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **sql_variant**  
  
## <a name="examples"></a>Exemplos  
### <a name="a-using-a-sql_variant-in-a-table"></a>a. Usando uma sql_variant em uma tabela  
 O exemplo a seguir recupera informações de `SQL_VARIANT_PROPERTY` sobre o valor de `colA``46279.1`, em que `colB` =`1689`, considerando que `tableA` tenha `colA` do tipo `sql_variant` e `colB`.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Observe que cada um desses três valores é uma **sql_variant**.  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sql_variant-as-a-variable"></a>B. Usando uma sql_variant como uma variável   
 O exemplo a seguir recupera informações de `SQL_VARIANT_PROPERTY` sobre uma variável chamada @v1.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  

