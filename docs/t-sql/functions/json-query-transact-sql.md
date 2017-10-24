---
title: JSON_QUERY (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 56b50c0497a2e0ee40f9cf086124eba8e55bdd03
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Extrai um objeto ou uma matriz de uma cadeia de caracteres JSON.  
  
 Para extrair um valor escalar de uma cadeia de caracteres JSON em vez de um objeto ou uma matriz, consulte [JSON_VALUE &#40; Transact-SQL &#41; ](../../t-sql/functions/json-value-transact-sql.md). Para obter informações sobre as diferenças entre **JSON_VALUE** e **JSON_QUERY**, consulte [comparar JSON_VALUE e JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 Uma expressão. Normalmente, o nome de uma variável ou uma coluna que contém o texto JSON.  
  
 Se **JSON_QUERY** localiza JSON não é válido em *expressão* antes de encontrar o valor identificado por *caminho*, a função retornará um erro. Se **JSON_QUERY** não encontrar o valor identificado por *caminho*, ele examina todo o texto e retorna um erro se ele encontrar JSON que não é válido em qualquer lugar na *expressão*.  
  
 *caminho*  
 Um caminho JSON que especifica o objeto ou matriz para extrair.

Em [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e em [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *caminho*.

O caminho JSON pode especificar o modo lax ou strict para análise. Se você não especificar o modo de análise, o modo incerto é o padrão. Para obter mais informações, consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  

O valor padrão para *caminho* é '$'. Como resultado, se você não fornecer um valor para *caminho*, **JSON_QUERY** retorna a entrada *expressão*.

Se o formato de *caminho* não é válido, **JSON_QUERY** retornará um erro.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um fragmento JSON do tipo nvarchar (max). O agrupamento do valor retornado é o mesmo que o agrupamento da expressão de entrada.  
  
 Se o valor não é um objeto ou uma matriz:  
  
-   No modo de lax **JSON_QUERY** retorna nulo.  
  
-   No modo estrito, **JSON_QUERY** retornará um erro.  
  
## <a name="remarks"></a>Comentários  

### <a name="lax-mode-and-strict-mode"></a>Modo incerto e modo estrito

 Considere o seguinte texto JSON:  
  
```json  
{
    "info": {
        "type": 1,
        "address": {
            "town": "Bristol",
            "county": "Avon",
            "country": "England"
        },
        "tags": ["Sport", "Water polo"]
    },
    "type": "Basic"
} 
```  
  
 A tabela a seguir compara o comportamento de **JSON_QUERY** no modo incerto e no modo estrito. Para obter mais informações sobre a especificação de modo de demarcador opcional (lax ou strict), consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Caminho|Valor de retorno no modo incerto|Valor de retorno no modo estrito|Obter mais informações|  
|----------|------------------------------|---------------------------------|---------------|  
|$|Retorna todo o texto JSON.|Retorna todo o texto JSON.|N/A|  
|$. info.type|NULL|Erro|Não um objeto ou matriz.<br /><br /> Use **JSON_VALUE** em vez disso.|  
|$. info.address.town|NULL|Erro|Não um objeto ou matriz.<br /><br /> Use **JSON_VALUE** em vez disso.|  
|$. Info." endereço"|N'{"cidade": "Bristol", "região": "Avon", "país": "Inglaterra"}'|N'{"cidade": "Bristol", "região": "Avon", "país": "Inglaterra"}'|N/A|  
|$. info.tags|N '["esporte", "Polo aquático"]'|N '["esporte", "Polo aquático"]'|N/A|  
|$. info.type[0]|NULL|Erro|Não é uma matriz.|  
|$. info.none|NULL|Erro|Propriedade não existe.|  

### <a name="using-jsonquery-with-for-json"></a>Usando JSON_QUERY com o FOR JSON

**JSON_QUERY** retorna um fragmento JSON válido. Como resultado, **FOR JSON** não escapar caracteres especiais no **JSON_QUERY** valor de retorno.

Se você estiver retornando resultados com o FOR JSON e você estiver incluindo dados que já está no formato JSON (em uma coluna ou como resultado de uma expressão), encapsule os dados JSON com **JSON_QUERY** sem o *caminho* parâmetro.

## <a name="examples"></a>Exemplos  
  
### <a name="example-1"></a>Exemplo 1  
 O exemplo a seguir mostra como retornar um fragmento JSON de um `CustomFields` coluna nos resultados da consulta.  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>Exemplo 2  
O exemplo a seguir mostra como incluir fragmentos JSON na saída da cláusula FOR JSON.  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões de caminho JSON &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Dados JSON &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  

