---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: daad1b738030efa48d5a85f91b70ebf747d4702c
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51812521"
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [Ajude a aprimorar os documentos do SQL Server!](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

Divide a expressão de caractere usando o separador especificado.  
  
> [!NOTE]  
> A função **STRING_SPLIT** está disponível somente no nível de compatibilidade 130 e superior. Se o nível de compatibilidade do banco de dados for inferior a 130, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá localizar nem executar a função **STRING_SPLIT**. Para alterar o nível de compatibilidade de um banco de dados, consulte [Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md).
> Observe que o nível de compatibilidade 120 pode ser padrão mesmo em novos [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>Argumentos  
 *cadeia de caracteres*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de caractere (ou seja, **nvarchar**, **varchar**, **nchar** ou **char**).  
  
 *separator*  
 É uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de caractere único de qualquer tipo de caractere (por exemplo, **nvarchar(1)**, **varchar(1)**, **nchar(1)** ou **char(1)**) usada como separador de cadeias de caracteres concatenadas.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna uma tabela de coluna única com fragmentos. O nome da coluna é **value**. Retorna **nvarchar** se um dos argumentos de entrada são **nvarchar** ou **nchar**. Caso contrário, retorna **varchar**. O tamanho do tipo de retorno é o mesmo que o tamanho do argumento da cadeia de caracteres.  
  
## <a name="remarks"></a>Remarks  
**STRING_SPLIT** usa uma cadeia de caracteres que deve ser dividida e o separador que será usado para dividir a cadeia de caracteres. Ele retorna uma tabela de coluna única com subcadeias de caracteres. Por exemplo, a seguinte instrução `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');` que usa o caractere de espaço como o separador, retorna a seguinte tabela de resultados:  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
  
Se a cadeia de caracteres de entrada é **NULL**, a função com valor de tabela **STRING_SPLIT** retorna uma tabela vazia.  
  
**STRING_SPLIT** exige, pelo menos, o modo de compatibilidade 130.  
  
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
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. Localizar linhas pela lista de valores  
Os desenvolvedores precisam criar uma consulta que localiza artigos por uma lista de IDs. Eles podem usar a seguinte consulta:  
  
```sql  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
Esse é o substituto de um antipadrão comum, como a criação de uma cadeia de caracteres SQL dinâmica na camada de aplicativo ou [!INCLUDE[tsql](../../includes/tsql-md.md)], ou com o uso do operador LIKE:  
  
```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>Consulte Também  
[LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)     
[LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)     
[RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)    
[RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)     
[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)     
[TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)     
[Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)      
  
  
