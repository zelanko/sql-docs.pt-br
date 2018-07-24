---
title: OPENJSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: douglasl
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: 55d9b3fcf3ab8e6b55c6704e363e486627f7985c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052912"
---
# <a name="openjson-transact-sql"></a>OPENJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON** é uma função com valor de tabela que analisa um texto JSON e retorna os objetos e as propriedades da entrada JSON como linhas e colunas. Em outras palavras, **OPENJSON** fornece uma exibição de conjunto de linhas em um documento JSON. Você pode especificar explicitamente as colunas no conjunto de linhas e os demarcadores de propriedades do JSON usados para popular as colunas. Como **OPENJSON** retorna um conjunto de linhas, você pode usar **OPENJSON** na cláusula `FROM` de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] exatamente como é usada qualquer outra tabela, exibição ou função com valor de tabela.  
  
Use **OPENJSON** para importar dados JSON no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou converter dados JSON em formato relacional para um aplicativo ou serviço que não possa consumir JSON diretamente.  
  
> [!NOTE]  
>  A função **OPENJSON** está disponível somente no nível de compatibilidade 130 ou superior. Se o nível de compatibilidade do banco de dados for inferior a 130, o SQL Server não poderá localizar e executar a função **OPENJSON**. Outras funções JSON estão disponíveis em todos os níveis de compatibilidade.
> 
> É possível verificar o nível de compatibilidade na exibição `sys.databases` ou nas propriedades do banco de dados. É possível alterar o nível de compatibilidade de um banco de dados usando o seguinte comando:  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>   
> O nível de compatibilidade 120 pode ser o padrão até mesmo em um novo Banco de Dados SQL do Azure.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico")[Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

A função com valor de tabela **OPENJSON** analisa a *jsonExpression* fornecida como o primeiro argumento e retorna uma ou mais linhas que contêm dados dos objetos JSON na expressão. *jsonExpression* pode conter subobjetos aninhados. Se você quiser analisar um subobjeto da *jsonExpression*, especifique um parâmetro **path** para o subobjeto JSON.

### <a name="openjson"></a>openjson

![Sintaxe do OPENJSON TVF](../../relational-databases/json/media/openjson-syntax.png "Sintaxe do OPENJSON")  

Por padrão, a função com valor de tabela **OPENJSON** retorna três colunas que contém o nome da chave, o valor e o tipo de cada par {key:value} encontrado na *jsonExpression*. Como alternativa, você pode especificar explicitamente o esquema do conjunto de resultados que o **OPENJSON** retorna fornecendo *with_clause*.
  
### <a name="withclause"></a>with_clause
  
![Sintaxe da cláusula WITH em OPENJSON TVF](../../relational-databases/json/media/openjson-shema-syntax.png "Sintaxe de OPENJSON WITH")

*with_clause* contém uma lista de colunas com seus tipos para **OPENJSON** retornar. Por padrão, **OPENJSON** faz a correspondência de chaves na *jsonExpression* com os nomes de coluna na *with_clause* (nesse caso, a correspondência de chave implica a diferenciação entre maiúsculas e minúsculas). Se um nome de coluna não corresponder a um nome de chave, você poderá fornecer um *column_path* opcional, que é uma [Expressão de demarcador JSON](../../relational-databases/json/json-path-expressions-sql-server.md) que referencia uma chave dentro da *jsonExpression*. 

## <a name="arguments"></a>Argumentos  
### <a name="jsonexpression"></a>*jsonExpression*  
Uma expressão de caractere Unicode que contém o texto JSON.  
  
OPENJSON itera sobre os elementos da matriz ou das propriedades do objeto na expressão de JSON e retorna uma linha para cada elemento ou propriedade. O exemplo a seguir retorna cada propriedade do objeto fornecido como *jsonExpression*:  
  
```sql  
DECLARE @json NVARCHAR(4000) = N'{  
   "StringValue":"John",  
   "IntValue":45,  
   "TrueValue":true,  
   "FalseValue":false,  
   "NullValue":null,  
   "ArrayValue":["a","r","r","a","y"],  
   "ObjectValue":{"obj":"ect"}  
}'

SELECT *
FROM OPENJSON(@json)
```  
  
**Resultados**  
  
|chave|value|Tipo|  
|---------|-----------|----------|  
|StringValue|John|1|  
|IntValue|45|2|  
|TrueValue|true|3|  
|FalseValue|false|3|  
|NullValue|NULL|0|  
|ArrayValue|["a","r","r","a","y"]|4|  
|ObjectValue|{"obj":"ect"}|5|  

### <a name="path"></a>*path*  
É uma expressão de caminho JSON opcional que referencia um objeto ou uma matriz na *jsonExpression*. **OPENJSON** busca no texto JSON na posição especificada e analisa apenas o fragmento referenciado. Para obter mais informações, confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).

No [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e no [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *path*.
  
O exemplo a seguir retorna um objeto aninhado ao especificar *path*:  

```sql  
DECLARE @json NVARCHAR(4000) = N'{  
      "path": {  
            "to":{  
                 "sub-object":["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]  
                 }  
              }  
 }';

SELECT [key], value
FROM OPENJSON(@json,'$.path.to."sub-object"')
```  
  
 **Resultados**  
  
|Chave|Valor|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
 
Quando **OPENJSON** analisa uma matriz JSON, a função retorna os índices dos elementos no texto JSON como chaves.

A comparação usada para corresponder as etapas do demarcador com as propriedades da expressão JSON diferencia maiúsculas de minúsculas e não reconhece agrupamento (ou seja, é uma comparação BIN2). 

### <a name="withclause"></a>*with_clause*
Define explicitamente o esquema de saída para a função **OPENJSON** retornar. A *with_clause* opcional pode conter os seguintes elementos:

*colName* É o nome da coluna de saída.  
  
Por padrão, **OPENJSON** usa o nome da coluna para corresponder a uma propriedade no texto JSON. Por exemplo, se você especificar a coluna *name* no esquema, OPENJSON tentará popular essa coluna com a propriedade "name" no texto JSON. Você pode substituir esse mapeamento padrão usando o argumento *column_path*.  
  
*tipo*  
É o tipo de dados da coluna de saída.  

> [!NOTE]
> Se você também usar a opção **AS JSON**, a coluna *type* precisará ser `NVARCHAR(MAX)`.
  
*column_path*  
É o caminho JSON que especifica a propriedade a ser retornada na coluna especificada. Para obter mais informações, consulte a descrição do parâmetro *path* anteriormente neste tópico.  
  
Use *column_path* para substituir as regras de mapeamento padrão quando o nome de uma coluna de saída não corresponder ao nome da propriedade.  
  
A comparação usada para corresponder as etapas do caminho com as propriedades da expressão JSON diferencia maiúsculas de minúsculas e não reconhece agrupamento (ou seja, é uma comparação BIN2).  
  
Para obter mais informações sobre os demarcadores, confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
*AS JSON*  
Use a opção **AS JSON** em uma definição de coluna para especificar que a propriedade referenciada contém um objeto JSON interno ou uma matriz. Se você especificar a opção **AS JSON**, o tipo da coluna precisará ser NVARCHAR(MAX).

-   Se você não especificar **AS JSON** para uma coluna, a função retornará um valor escalar (por exemplo, int, cadeia de caracteres, true, false) da propriedade JSON especificada no caminho especificado. Se o caminho representar um objeto ou uma matriz e a propriedade não puder ser encontrada no caminho especificado, a função retornará nula no modo incerto ou retornará um erro no modo estrito. Esse comportamento é semelhante ao comportamento da função **JSON_VALUE**.  
  
-   Se você especificar **AS JSON** para uma coluna, a função retornará um fragmento JSON da propriedade JSON especificada no caminho especificado. Se o demarcador representar um valor escalar e a propriedade não puder ser encontrada no demarcador especificado, a função retornará um nula no modo incerto ou retornará um erro no modo estrito. Esse comportamento é semelhante ao comportamento da função **JSON_QUERY**.  
  
> [!NOTE]  
> Se você quiser retornar um fragmento JSON aninhado de uma propriedade JSON, forneça o sinalizador **AS JSON**. Sem essa opção, se a propriedade não puder ser encontrada, OPENJSON retornará um valor NULL em vez da matriz ou do objeto JSON referenciado ou retornará um erro em tempo de execução no modo estrito.  
  
Por exemplo, a consulta a seguir retorna e formata os elementos de uma matriz:  
  
```sql  
DECLARE @json NVARCHAR(MAX) = N'[  
  {  
    "Order": {  
      "Number":"SO43659",  
      "Date":"2011-05-31T00:00:00"  
    },  
    "AccountNumber":"AW29825",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":1  
    }  
  },  
  {  
    "Order": {  
      "Number":"SO43661",  
      "Date":"2011-06-01T00:00:00"  
    },  
    "AccountNumber":"AW73565",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":3  
    }  
  }
]'  
   
SELECT *
FROM OPENJSON ( @json )  
WITH (   
              Number   varchar(200)   '$.Order.Number',  
              Date     datetime       '$.Order.Date',  
              Customer varchar(200)   '$.AccountNumber',  
              Quantity int            '$.Item.Quantity',  
              [Order]  nvarchar(MAX)  AS JSON  
 )
```  
  
**Resultados**  
  
|Número|data|Cliente|Quantidade|Order|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|{"Number":"SO43659","Date":"2011-05-31T00:00:00"}|  
|SO43661|2011-06-01T00:00:00|AW73565|3|{"Number":"SO43661","Date":"2011-06-01T00:00:00"}|  
  

## <a name="return-value"></a>Valor retornado  
As colunas que a função OPENJSON retorna dependem da opção WITH.  
  
1. Quando você chama OPENJSON com o esquema padrão, ou seja, sem especificar um esquema explícito na cláusula WITH, a função retorna uma tabela com as seguintes colunas:  
    1.  **Key**. Um valor nvarchar(4000) que contém o nome da propriedade especificada ou o índice do elemento na matriz especificada. A coluna de chave tem um agrupamento BIN2.  
    2.  **Valor**. Um valor nvarchar(max) que contém o valor da propriedade. A coluna de valor herda seu agrupamento de *jsonExpression*.
    3.  **Type**. Um valor inteiro que contém o tipo do valor. A coluna **Type** é retornada somente quando você usa OPENJSON com o esquema padrão. A coluna de tipo tem um dos seguintes valores:  
  
        |Valor da coluna Type|Tipo de dados JSON|  
        |------------------------------|--------------------|  
        |0|nulo|  
        |1|cadeia de caracteres|  
        |2|INT|  
        |3|true/false|  
        |4|matriz|  
        |5|objeto|  
  
     Somente propriedades de primeiro nível são retornadas. A instrução falhará se o texto JSON não estiver formatado corretamente.  

2. Quando você chama OPENJSON e especifica um esquema explícito na cláusula WITH, a função retorna uma tabela com o esquema definido na cláusula WITH.  

## <a name="remarks"></a>Remarks  

*json_path* usado no segundo argumento de **OPENJSON** ou em *with_clause* pode iniciar com a palavra-chave **lax** ou **strict**.

-   No modo **incerto**, **OPENJSON** não gera um erro quando o objeto ou o valor no demarcador especificado não pode ser encontrado. Se o demarcador não puder ser encontrado, **OPENJSON** retornará um conjunto de resultados vazio ou um valor NULL.
-   No modo **estrito**, **OPENJSON** retornará um erro se o demarcador não puder ser encontrado.

Alguns dos exemplos nesta página especificam explicitamente o modo de demarcador, ou seja, incerto ou estrito. O modo de demarcador é opcional. Se você não especificar explicitamente o modo de demarcador, o modo incerto será o padrão. Para obter mais informações sobre o modo de demarcador e as expressões de demarcador, confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).    

Os nomes de coluna em *with_clause* são correspondidos às chaves no texto JSON. Se você especificar o nome da coluna `[Address.Country]`, ele será correspondido com a chave `Address.Country`. Se você quiser referenciar uma chave aninhada `Country` dentro do objeto `Address`, especifique o demarcador `$.Address.Country` no demarcador da coluna.

*json_path* podem conter chaves com caracteres alfanuméricos. Coloque o nome da chave em *json_path* entre aspas duplas se houver caracteres especiais nas chaves. Por exemplo, `$."my key $1".regularKey."key with . dot"` corresponde ao valor 1 no seguinte texto JSON:

```json
{
  "my key $1": {
    "regularKey":{
      "key with . dot": 1
    }
  }
}
```  

## <a name="examples"></a>Exemplos  
  
### <a name="example-1---convert-a-json-array-to-a-temporary-table"></a>Exemplo 1: converter uma matriz JSON em uma tabela temporária  
O exemplo a seguir fornece uma lista de identificadores como uma matriz JSON de números. A consulta converte a matriz JSON em uma tabela de identificadores e filtra todos os produtos com as IDs especificadas.  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
Esta consulta é equivalente ao exemplo a seguir. No entanto, no exemplo abaixo, você precisa inserir números na consulta em vez de passá-los como parâmetros.  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>Exemplo 2: mesclar propriedades de dois objetos JSON  
O exemplo a seguir seleciona uma união de todas as propriedades de dois objetos JSON. Os dois objetos têm uma propriedade *name* duplicada. O exemplo usa o valor da chave para excluir a linha duplicada dos resultados.  
  
```sql  
DECLARE @json1 NVARCHAR(MAX),@json2 NVARCHAR(MAX)

SET @json1=N'{"name": "John", "surname":"Doe"}'

SET @json2=N'{"name": "John", "age":45}'

SELECT *
FROM OPENJSON(@json1)
UNION ALL
SELECT *
FROM OPENJSON(@json2)
WHERE [key] NOT IN (SELECT [key] FROM OPENJSON(@json1))
```  
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>Exemplo 3: unir linhas com os dados JSON armazenados em células de tabela usando CROSS APPLY  
No exemplo a seguir, a tabela `SalesOrderHeader` tem uma coluna de texto `SalesReason` que contém uma matriz de `SalesOrderReasons` no formato JSON. Os objetos `SalesOrderReasons` contêm propriedades como *Quality* e *Manufacturer*. O exemplo cria um relatório que une cada linha da ordem de venda aos motivos de vendas relacionados. O operador OPENJSON expande a matriz JSON de motivos de vendas como se os motivos estivessem armazenados em uma tabela filha separada. Em seguida, o operador CROSS APPLY une cada linha da ordem de venda às linhas retornadas pela função com valor de tabela OPENJSON.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> Quando é necessário expandir matrizes JSON armazenadas em campos individuais e uni-las às suas linhas pai, normalmente se usa o operador [!INCLUDE[tsql](../../includes/tsql-md.md)] CROSS APPLY. Para obter mais informações sobre CROSS APPLY, confira [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
A mesma consulta pode ser reescrita usando `OPENJSON` com um esquema de linhas definido explicitamente a ser retornado:  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
Neste exemplo, o demarcador `$` referencia cada elemento da matriz. Se você quiser converter explicitamente o valor retornado, use esse tipo de consulta.  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>Exemplo 4: combinar linhas relacionais e elementos JSON com CROSS APPLY  
A consulta a seguir combina as linhas relacionais e os elementos JSON nos resultados mostrados na tabela a seguir.  
  
```sql  
SELECT store.title, location.street, location.lat, location.long  
FROM store  
CROSS APPLY OPENJSON(store.jsonCol, 'lax $.location')   
     WITH (street varchar(500) ,  postcode  varchar(500) '$.postcode' ,  
     lon int '$.geo.longitude', lat int '$.geo.latitude')  
     AS location
```  
  
**Resultados**  
  
|title|street|postcode|lon|lat|  
|-----------|------------|--------------|---------|---------|  
|Whole Food Markets|17991 Redmond Way|WA 98052|47.666124|-122.10155|  
|Sears|148th Ave NE|WA 98052|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>Exemplo 5: importar dados JSON no SQL Server  
O exemplo a seguir carrega um objeto JSON inteiro em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```sql  
DECLARE @json NVARCHAR(max)  = N'{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50))
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Converter dados JSON em linhas e colunas com OPENJSON &#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [Usar OPENJSON com o esquema padrão &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [Usar OPENJSON com um esquema explícito &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
  
