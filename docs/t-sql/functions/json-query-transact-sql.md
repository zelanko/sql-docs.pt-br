---
title: JSON_QUERY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 5acf669e6db68b5fceb3a83c7f036d5f8065bde3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752253"
---
# <a name="json_query-transact-sql"></a>JSON_QUERY (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

 Extrai um objeto ou uma matriz de uma cadeia de caracteres JSON.  
  
 Para extrair um valor escalar de uma cadeia de caracteres JSON em vez de um objeto ou uma matriz, confira [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md). Para obter informações sobre as diferenças entre **JSON_VALUE** e **JSON_QUERY**, confira [Comparar JSON_VALUE e JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>Argumentos

 *expressão*  
 Uma expressão. Normalmente, o nome de uma variável ou de uma coluna que contém o texto JSON.  
  
 Se **JSON_QUERY** localizar um JSON que não seja válido na *expressão* antes de encontrar o valor identificado por *path*, a função retornará um erro. Se **JSON_QUERY** não encontrar o valor identificado por *path*, ele verificará todo o texto e retornará um erro se encontrar um JSON que não seja válido em algum lugar na *expressão*.  
  
 *path*  
 Um demarcador JSON que especifica o objeto ou a matriz a ser extraída.

No [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e no [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *path*.

O demarcador JSON pode especificar o modo incerto ou estrito para análise. Se você não especificar o modo de análise, o modo incerto será o padrão. Para obter mais informações, confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  

O valor padrão para *path* é '$'. Como resultado, se você não fornecer um valor para *path*, **JSON_QUERY** retornará a *expressão* de entrada.

Se o formato de *path* não for válido, **JSON_QUERY** retornará um erro.  
  
## <a name="return-value"></a>Valor retornado

 Retorna um fragmento JSON do tipo nvarchar(max). A ordenação do valor retornado é a mesma que a ordenação da expressão de entrada.  
  
 Se o valor não for um objeto nem uma matriz:  
  
- No modo incerto **JSON_QUERY** retornará nulo.  
  
- No modo estrito, **JSON_QUERY** retornará um erro.  
  
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
  
 A tabela a seguir compara o comportamento de **JSON_QUERY** no modo incerto e no modo estrito. Para obter mais informações sobre a especificação de modo de demarcador opcional (incerto ou estrito), confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Caminho|Valor retornado no modo incerto|Valor retornado no modo estrito|Obter mais informações|  
|----------|------------------------------|---------------------------------|---------------|  
|$|Retorna o texto JSON inteiro.|Retorna o texto JSON inteiro.|N/A|  
|$.info.type|NULO|Erro|Não é um objeto nem uma matriz.<br /><br /> Use **JSON_VALUE** nesse caso.|  
|$.info.address.town|NULO|Erro|Não é um objeto nem uma matriz.<br /><br /> Use **JSON_VALUE** nesse caso.|  
|$.info."address"|N'{ "town":"Bristol", "county":"Avon", "country":"England" }'|N'{ "town":"Bristol", "county":"Avon", "country":"England" }'|N/A|  
|$.info.tags|N'[ "Sport", "Water polo"]'|N'[ "Sport", "Water polo"]'|N/A|  
|$.info.type[0]|NULO|Erro|Não é uma matriz.|  
|$.info.none|NULO|Erro|A propriedade não existe.|  

### <a name="using-json_query-with-for-json"></a>Usando JSON_QUERY com FOR JSON

**JSON_QUERY** retorna um fragmento JSON válido. Como resultado, **FOR JSON** não usa escape para caracteres especiais no valor retornado de **JSON_QUERY**.

Se você estiver retornando resultados com FOR JSON e estiver incluindo dados que já estejam no formato JSON (em uma coluna ou como resultado de uma expressão), encapsule os dados JSON com **JSON_QUERY** sem o parâmetro *path*.

## <a name="examples"></a>Exemplos  
  
### <a name="example-1"></a>Exemplo 1

 O exemplo a seguir mostra como retornar um fragmento JSON de uma coluna `CustomFields` nos resultados da consulta.  
  
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
  
## <a name="see-also"></a>Confira também

- [Expressões de caminho JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
- [Dados JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
