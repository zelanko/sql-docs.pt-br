---
title: sql_variant (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6a417d8240bb3360a13367230f0017762b51d659
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68000508"
---
# <a name="sql_variant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Um tipo de dados que armazena valores de vários tipos de dados com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>Comentários  
**sql_variant** pode ser usado em colunas, parâmetros, variáveis e nos valores retornados de funções definidas pelo usuário. **sql_variant** permite que esses objetos de banco de dados sejam compatíveis com valores de outros tipos de dados.
  
Uma coluna do tipo **sql_variant** pode conter linhas de tipos de dados diferentes. Por exemplo, uma coluna definida como **sql_variant** pode armazenar valores **int**, **binary** e **char**.
  
**sql_variant** pode ter um comprimento máximo de 8016 bytes. Isso inclui as informações de tipo base e o valor de tipo base. O tamanho máximo do valor de tipo base atual é 8.000 bytes.
  
Um tipo de dados **sql_variant** deve primeiro ser convertido em seu valor de tipo de dados base antes de participar de operações como adição e subtração.
  
É possível atribuir um valor padrão a **sql_variant**. Esse tipo de dados pode também ter NULL como valor subjacente, mas os valores NULL não terão um tipo base associado. Além disso, **sql_variant** não pode ter outra **sql_variant** como seu tipo base.
  
Uma chave primária exclusiva ou chave estrangeira pode incluir colunas do tipo **sql_variant**, mas o tamanho total dos valores de dados que constituem a chave de uma linha específica não deve ser superior ao tamanho máximo de um índice. Esse é de 900 bytes.
  
Uma tabela pode ter qualquer número de colunas **sql_variant**.
  
Não é possível usar **sql_variant** em CONTAINSTABLE e FREETEXTTABLE.
  
ODBC não é totalmente compatível com **sql_variant**. Desse modo, as consultas de colunas **sql_variant** retornam como valores binários quando você usa o MSDASQL (Provedor Microsoft OLE DB para ODBC). Por exemplo, uma coluna **sql_variant** que contém os dados de cadeia de caracteres 'PS2091' retorna como 0x505332303931.
  
## <a name="comparing-sql_variant-values"></a>Comparando valores sql_variant  
O tipo de dados **sql_variant** pertence ao topo da lista de hierarquia de tipo de dados para conversão. Para comparações de **sql_variant**, a ordem da hierarquia de tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é agrupada em famílias de tipos de dados.
  
|Hierarquia de tipos de dados|Família de tipos de dados|  
|---|---|
|**sql_variant**|sql_variant |  
|**datetime2**|Data e hora|  
|**datetimeoffset**|Data e hora|  
|**datetime**|Data e hora|  
|**smalldatetime**|Data e hora|  
|**date**|Data e hora|  
|**time**|Data e hora|  
|**float**|Numérico aproximado|  
|**real**|Numérico aproximado|  
|**decimal**|Numérico exato|  
|**money**|Numérico exato|  
|**smallmoney**|Numérico exato|  
|**bigint**|Numérico exato|  
|**int**|Numérico exato|  
|**smallint**|Numérico exato|  
|**tinyint**|Numérico exato|  
|**bit**|Numérico exato|  
|**nvarchar**|Unicode|  
|**nchar**|Unicode|  
|**varchar**|Unicode|  
|**char**|Unicode|  
|**varbinary**|Binário|  
|**binary**|Binário|  
|**uniqueidentifier**|Uniqueidentifier |  
  
As seguintes regras se aplicam a comparações **sql_variant**:
-   Quando valores de **sql_variant** de diferentes tipos de dados base são comparados e os tipos de dados base estão em diferentes famílias de tipos de dados, o valor cuja família de tipo de dados aparece no topo do gráfico da hierarquia é considerado o mais alto dos dois valores.  
-   Quando valores de **sql_variant** de diferentes tipos de dados base são comparados e os tipos de dados base estão na mesma família de tipos de dados, o valor cujo tipo de dados base está na parte mais inferior do gráfico da hierarquia é convertido implicitamente no outro tipo de dados e a comparação é feita.  
-   Quando valores **sql_variant** de **char**, **varchar**, **nchar**, ou **nvarchar** são de tipos de dados em comparação, suas ordenações são primeiro comparadas com base nos seguintes critérios: LCID, versão do LCID, sinalizadores de comparação e ID de classificação. Todos esses critérios são comparados como valores de inteiro na ordem listada. Se todos esses critérios forem iguais, os valores reais da cadeia de caracteres serão comparados de acordo com a ordenação.  
  
## <a name="converting-sql_variant-data"></a>Convertendo dados sql_variant  
Ao lidar com o tipo de dados **sql_variant**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é compatível com conversões implícitas de objetos com outros tipos de dados para o tipo **sql_variant**. Entretanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte para conversões implícitas de dados **sql_variant** para um objeto com outro tipo de dados.
  
## <a name="restrictions"></a>Restrições  
A tabela a seguir lista os tipos de valores que não podem ser armazenados usando **sql_variant**:
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**imagem**|**rowversion** (**timestamp**)|  
|**sql_variant**|**geografia**|  
|**hierarchyid**|**geometria**|  
|Tipos definidos pelo usuário|**datetimeoffset**<sup>1</sup>| 

<sup>1</sup> O SQL Server 2012 e posterior não restringem **datetimeoffset**.

## <a name="examples"></a>Exemplos  

### <a name="a-using-a-sql_variant-in-a-table"></a>a. Usando uma sql_variant em uma tabela  
 O exemplo a seguir cria uma tabela com um tipo de dados sql_variant. Então o exemplo recupera informações `SQL_VARIANT_PROPERTY` sobre o valor de `colA``46279.1`, em que `colB` =`1689`, supondo que `tableA` tenha `colA` do tipo `sql_variant` e `colB`.  
  
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
 O exemplo a seguir, cria uma variável usando o tipo de dados sql_variant e, em seguida, recupera informações `SQL_VARIANT_PROPERTY` sobre uma variável chamada @v1.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```    


## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  
