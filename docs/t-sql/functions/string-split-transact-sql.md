---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current||=azure-sqldw-latest||>= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: aab93a133a8dcfeaea96ffa1886ccfcb20936f95
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947481"
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Uma função com valor de tabela que divide uma cadeia de caracteres em linhas de subcadeias de caracteres com base em um caractere separador especificado.

#### <a name="compatibility-level-130"></a>Nível de compatibilidade 130

STRING_SPLIT requer que o nível de compatibilidade seja, no mínimo, 130. Quando o nível for inferior a 130, o SQL Server não conseguirá localizar a função STRING_SPLIT.

Para alterar o nível de compatibilidade de um banco de dados, consulte [Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  

```sql
STRING_SPLIT ( string , separator )  
```

## <a name="arguments"></a>Argumentos

 *cadeia de caracteres*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de caractere (ou seja, **nvarchar**, **varchar**, **nchar** ou **char**).  
  
 *separator*  
 É uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de caractere único de qualquer tipo de caractere (por exemplo, **nvarchar(1)** , **varchar(1)** , **nchar(1)** ou **char(1)** ) usada como separador de subcadeias de caracteres concatenadas.  
  
## <a name="return-types"></a>Tipos de retorno  

Retorna uma tabela de coluna única cujas linhas são as subcadeias de caracteres. O nome da coluna é **value**. Retorna **nvarchar** se um dos argumentos de entrada são **nvarchar** ou **nchar**. Caso contrário, retorna **varchar**. O tamanho do tipo de retorno é o mesmo que o tamanho do argumento da cadeia de caracteres.  
  
## <a name="remarks"></a>Remarks  

**STRING_SPLIT** insere uma cadeia de caracteres que tem subcadeias de caracteres delimitadas e insere um caractere a ser usado como separador ou delimitador. STRING_SPLIT gera uma tabela de coluna única cujas linhas contêm as subcadeias de caracteres. O nome da coluna de saída é **value**.

As linhas de saída podem estar em outra ordem. A ordem _não_ é a garantia de corresponder à ordem das subcadeias de caracteres na cadeia de caracteres de entrada. É possível substituir a ordem de classificação final usando uma cláusula ORDER BY na instrução SELECT (`ORDER BY value`).

Subcadeias de caracteres de comprimento zero vazias estão presentes quando a cadeia de caracteres de entrada contém duas ou mais ocorrências consecutivas do caractere delimitador. As subcadeias de caracteres vazias são tratadas da mesma forma que são as subcadeias de caracteres sem formatação. É possível filtrar as linhas que contêm a subcadeia de caracteres vazia usando a cláusula WHERE (`WHERE value <> ''`). Se a cadeia de caracteres de entrada for NULL, a função com valor de tabela STRING_SPLIT retornará uma tabela vazia.  

Por exemplo, a seguinte instrução SELECT usa o caractere de espaço como o separador:

```sql
SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');
```

Na prática, a SELECT anterior retornava a seguinte tabela de resultado:  
  
|value|  
| :-- |  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
| &nbsp; |

## <a name="examples"></a>Exemplos  
  
### <a name="a-split-comma-separated-value-string"></a>A. Dividir uma cadeia de caracteres de valores separados por vírgula

Analise uma lista separada por vírgulas de valores e retorne todos os tokens não vazios:  

```sql
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';
```

STRING_SPLIT retornará a cadeia de caracteres vazia se não houver nada entre o separador. A condição RTRIM(value) <> '' removerá tokens vazios.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. Dividir uma cadeia de caracteres de valores separados por vírgula em uma coluna

A tabela Product tem uma coluna com uma lista separada por vírgula de marcas mostradas no seguinte exemplo:  
  
|ProductId|Nome|Marcas|  
|---------------|----------|----------|  
|1|Full-Finger Gloves|clothing, road, touring, bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike, mountain|  
  
A seguinte consulta transforma cada lista de marcas e une-as com a linha original:  

```sql  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|Nome|value|  
|---------------|----------|-----------|  
|1|Full-Finger Gloves|clothing|  
|1|Full-Finger Gloves|road|  
|1|Full-Finger Gloves|touring|  
|1|Full-Finger Gloves|bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  

  >[!NOTE]
  > A ordem da saída pode variar, uma vez que _não_ há garantia de que a ordem corresponda à ordem das subcadeias de caracteres na cadeia de entrada.
  
### <a name="c-aggregation-by-values"></a>C. Agregação por valores

Os usuários precisam criar um relatório que mostra o número de produtos por marca, ordenado pelo número de produtos, e filtrar apenas as marcas com mais de dois produtos.  

```sql  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```

### <a name="d-search-by-tag-value"></a>D. Pesquisar por valor de marca

Os desenvolvedores precisam criar consultas que localizam artigos por palavras-chave. Eles podem usar as seguintes consultas:  
  
Para localizar produtos com uma única marca (clothing):  

```sql
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```

Localize produtos com duas marcas especificadas (clothing e road):  

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road'));  
```

### <a name="e-find-rows-by-list-of-values"></a>E. Localizar linhas pela lista de valores

Os desenvolvedores precisam criar uma consulta que localiza artigos por uma lista de IDs. Eles podem usar a seguinte consulta:  

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')
    ON value = ProductId;  
```  

O uso de STRING_SPLIT anterior é uma substituição para um antipadrão comum. Esse antipadrão pode envolver a criação de uma cadeia de caracteres SQL dinâmica na camada de aplicativo ou no Transact-SQL. Ou um antipadrão pode ser obtido usando o operador LIKE. Confira a seguinte instrução SELECT de exemplo:

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```

## <a name="see-also"></a>Consulte Também

[LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)<br />
[LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)<br />
[RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)<br />
[RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)<br />
[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)<br />
[TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)<br />
[Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
