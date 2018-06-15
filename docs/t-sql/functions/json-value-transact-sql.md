---
title: JSON_VALUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
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
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: 9bbd4dd23c4c536fa70f679ceabf6d96ddde121c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33054623"
---
# <a name="jsonvalue-transact-sql"></a>JSON_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Extrai um valor escalar de uma cadeia de caracteres JSON.  
  
 Para extrair um objeto ou uma matriz de uma cadeia de caracteres JSON em vez de um valor escalar, confira [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md). Para obter informações sobre as diferenças entre **JSON_VALUE** e **JSON_QUERY**, confira [Comparar JSON_VALUE e JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 Uma expressão. Normalmente, o nome de uma variável ou de uma coluna que contém o texto JSON.  
 
 Se **JSON_VALUE** localizar um JSON que não seja válido na *expressão* antes de localizar o valor identificado por *path*, a função retornará um erro. Se **JSON_VALUE* não localizar o valor identificado por *path*, ele examinará todo o texto e retornará um erro se localizar um JSON que não seja válido em nenhum lugar na *expressão*.
  
 *path*  
 Um demarcador JSON que especifica a propriedade a ser extraída. Para obter mais informações, confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
 
No [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e no [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *path*.
  
 Se o formato de *path* não for válido, **JSON_VALUE** retornará um erro.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor de texto único do tipo nvarchar(4000). O agrupamento do valor retornado é o mesmo que o agrupamento da expressão de entrada.  
  
 Se o valor tiver mais que 4000 caracteres:  
  
-   No modo incerto **JSON_VALUE** retorna nulo.  
  
-   No modo estrito, **JSON_VALUE** retorna um erro.  
  
 Se você precisar retornar valores escalares com mais de 4000 caracteres, use **OPENJSON** em vez de **JSON_VALUE**. Para obter mais informações, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="remarks"></a>Remarks

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
  
 A tabela a seguir compara o comportamento de **JSON_VALUE** no modo incerto e no modo estrito. Para obter mais informações sobre a especificação de modo de demarcador opcional (incerto ou estrito), confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Caminho|Valor retornado no modo incerto|Valor retornado no modo estrito|Obter mais informações|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** nesse caso.|  
|$.info.type|N'1'|N'1'|N/A|  
|$.info.address.town|N'Bristol'|N'Bristol'|N/A|  
|$.info."address"|NULL|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** nesse caso.|  
|$.info.tags|NULL|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** nesse caso.|  
|$.info.type[0]|NULL|Erro|Não é uma matriz.|  
|$.info.none|NULL|Erro|A propriedade não existe.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="example-1"></a>Exemplo 1  
 O exemplo a seguir usa os valores das propriedades JSON `town` e `state` nos resultados da consulta. Como **JSON_VALUE** preserva o agrupamento da origem, a ordem de classificação dos resultados depende do agrupamento da coluna `jsonInfo`. 

> [!NOTE]
> (Este exemplo assume que uma tabela denominada `Person.Person` contém uma coluna `jsonInfo` de texto JSON e que essa coluna tem a estrutura mostrada anteriormente na discussão sobre modo incerto e modo estrito. No banco de dados AdventureWorks de exemplo, a tabela `Person` realmente não contém uma coluna `jsonInfo`.)
  
```sql  
SELECT FirstName, LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>Exemplo 2  
 O exemplo a seguir extrai o valor da propriedade JSON `town` para uma variável local.  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'<array of address info>'

SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')
```  
  
### <a name="example-3"></a>Exemplo 3  
 O exemplo a seguir cria as colunas computadas com base nos valores das propriedades JSON.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Dados JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
