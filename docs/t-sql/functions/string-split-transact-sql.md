---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 049bdf1021d57e28ed94e11c89aa997ee0eba5e5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Divide a expressão de caractere usando o separador especificado.  
  
> [!NOTE]  
>  O **STRING_SPLIT** função está disponível somente no nível de compatibilidade 130. Se o nível de compatibilidade do banco de dados for inferior a 130, do SQL Server não será capaz de localizar e executar **STRING_SPLIT** função. Você pode alterar um nível de compatibilidade do banco de dados usando o seguinte comando:  
> ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
>   
>  Observe que o nível de compatibilidade 120 pode ser padrão mesmo em novos bancos de dados do SQL do Azure.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>Argumentos  
 *cadeia de caracteres*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de caractere (isto é, **nvarchar**, **varchar**, **nchar** ou **char**).  
  
 *separador*  
 É um caractere único [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de caractere (por exemplo, **nvarchar(1)**, **varchar (1)**, **nchar (1)** ou  **char (1)**) que é usado como separador de cadeias de caracteres concatenadas.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna uma tabela de coluna única com fragmentos. O nome da coluna é **valor**. Retorna **nvarchar** se qualquer um dos argumentos de entrada são **nvarchar** ou **nchar**. Caso contrário, retornará **varchar**. O comprimento do tipo de retorno é o mesmo que o comprimento do argumento da cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 **STRING_SPLIT** usa uma cadeia de caracteres que deve ser dividida e o separador que será usado para dividir a cadeia de caracteres. Retorna uma tabela de coluna única com subcadeias de caracteres. Por exemplo, a instrução a seguir `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');` usando o caractere de espaço como separador de retorna resultados de tabela a seguir:  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|SIT|  
|Amet.|  
  
 Se a cadeia de caracteres de entrada é **nulo**, o **STRING_SPLIT** função com valor de tabela retorna uma tabela vazia.  
  
 **STRING_SPLIT** requer pelo menos o modo de compatibilidade 130.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-split-comma-separated-value-string"></a>A. Divisão CSV que a cadeia de caracteres de valor  
 Analisar uma lista separada por vírgulas de valores e retornar todos os tokens de não vazio:  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 STRING_SPLIT retornará a cadeia de caracteres vazia se não houver nada entre separador. Condição RTRIM(value) <> ' removerá tokens vazios.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. Divisão CSV que a cadeia de caracteres de valor em uma coluna  
 Tabela Product tem uma coluna com a lista separada por vírgulas de marcas mostrado no exemplo a seguir:  
  
|productId|Nome|Marcas|  
|---------------|----------|----------|  
|1|Luvas de dedo|roupas, road, Bicicletas de passeio,|  
|2|LL fone|Bicicleta|  
|3|HL Mountain Frame|bicicleta, mountain|  
  
 Consulta a seguir transforma cada lista de marcas e une com a linha original:  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|productId|Nome|value|  
|---------------|----------|-----------|  
|1|Luvas de dedo|roupas|  
|1|Luvas de dedo|Road|  
|1|Luvas de dedo|Passeio|  
|1|Luvas de dedo|Bicicleta|  
|2|LL fone|Bicicleta|  
|3|HL Mountain Frame|Bicicleta|  
|3|HL Mountain Frame|Mountain|  
  
### <a name="c-aggregation-by-values"></a>C. Agregação de valores  
 Os usuários devem criar um relatório que mostra o número de produtos por cada marca, ordenados pelo número de produtos e para filtrar apenas as marcas com mais de 2 produtos.  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. Pesquisar por valor de marca  
 Os desenvolvedores devem criar consultas que encontrar artigos por palavras-chave. Eles podem usar consultas a seguir:  
  
 Para localizar produtos com uma única marca (roupas):  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 Localize os produtos com duas marcas especificados (roupas e road):  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. Localizar linhas pela lista de valores  
 Os desenvolvedores devem criar uma consulta que encontra artigos por uma lista de ids. Eles podem usar a seguinte consulta:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 Isso é o substituto do anticomum padrão de, como a criação de uma cadeia de caracteres SQL dinâmica na camada de aplicativo ou [!INCLUDE[tsql](../../includes/tsql-md.md)], ou usando o operador LIKE:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Subcadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

