---
title: JSON_VALUE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ebb940035e4cad1ef898cfe83e1932db573848ab
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="jsonvalue-transact-sql"></a>JSON_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Extrai um valor escalar de uma cadeia de caracteres JSON.  
  
 Para extrair um objeto ou uma matriz de uma cadeia de caracteres JSON em vez de um valor escalar, consulte [JSON_QUERY &#40; Transact-SQL &#41; ](../../t-sql/functions/json-query-transact-sql.md). Para obter informações sobre as diferenças entre **JSON_VALUE** e **JSON_QUERY**, consulte [comparar JSON_VALUE e JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 Uma expressão. Normalmente, o nome de uma variável ou uma coluna que contém o texto JSON.  
 
 Se **JSON_VALUE** localiza JSON não é válido em *expressão* antes de encontrar o valor identificado por *caminho*, a função retornará um erro. Se **JSON_VALUE* não encontrar o valor identificado por *caminho*, ele examina todo o texto e retorna um erro se ele encontrar JSON que não é válido em qualquer lugar na *expressão*.
  
 *caminho*  
 Um caminho JSON que especifica a propriedade para extrair. Para obter mais informações, consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
 
Em [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e em [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *caminho*.
  
 Se o formato de *caminho* não é válido, **JSON_VALUE** retornará um erro.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor de texto única do tipo nvarchar (4000). O agrupamento do valor retornado é o mesmo que o agrupamento da expressão de entrada.  
  
 Se o valor for maior que 4000 caracteres:  
  
-   No modo de lax **JSON_VALUE** retorna nulo.  
  
-   No modo estrito, **JSON_VALUE** retornará um erro.  
  
 Se você tiver que retornam valores escalares maior que 4000 caracteres, use **OPENJSON** em vez de **JSON_VALUE**. Para obter mais informações, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="remarks"></a>Comentários

### <a name="lax-mode-and-strict-mode"></a>Modo incerto e modo estrito

 Considere o seguinte texto JSON:  
  
```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'  
```  
  
 A tabela a seguir compara o comportamento de **JSON_VALUE** no modo incerto e no modo estrito. Para obter mais informações sobre a especificação de modo de demarcador opcional (lax ou strict), consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Caminho|Valor de retorno no modo incerto|Valor de retorno no modo estrito|Obter mais informações|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** em vez disso.|  
|$. info.type|N '1'|N '1'|N/A|  
|$. info.address.town|N'Bristol'|N'Bristol'|N/A|  
|$. Info." endereço"|NULL|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** em vez disso.|  
|$. info.tags|NULL|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** em vez disso.|  
|$. info.type[0]|NULL|Erro|Não é uma matriz.|  
|$. info.none|NULL|Erro|Propriedade não existe.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="example-1"></a>Exemplo 1  
 O exemplo a seguir usa os valores das propriedades JSON `town` e `state` nos resultados da consulta. Como **JSON_VALUE** preserva o agrupamento de origem, a ordem de classificação dos resultados depende do agrupamento do `jsonInfo` coluna.  
  
```sql  
SELECT FirstName,LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>Exemplo 2  
 O exemplo a seguir extrai o valor da propriedade JSON `town` em uma variável local.  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'<array of address info>'

SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')
```  
  
### <a name="example-3"></a>Exemplo 3  
 O exemplo a seguir cria as colunas computadas com base nos valores de propriedades JSON.  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(8000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões de caminho JSON &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Dados JSON &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

