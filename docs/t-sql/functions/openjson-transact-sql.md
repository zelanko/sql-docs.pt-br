---
title: OPENJSON (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 936a53d9174b199860432e0cfcb9c8add97529ca
ms.contentlocale: pt-br
ms.lasthandoff: 09/19/2017

---
# <a name="openjson-transact-sql"></a>OPENJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON** é uma função com valor de tabela que analisa texto JSON e retorna os objetos e propriedades da entrada JSON como linhas e colunas. Em outras palavras, **OPENJSON** fornece uma exibição de conjunto de linhas em um documento JSON. Você pode especificar explicitamente as colunas no conjunto de linhas e os caminhos de propriedade JSON usados para preencher as colunas. Como **OPENJSON** retorna um conjunto de linhas, você pode usar **OPENJSON** no `FROM` cláusula de um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução exatamente como você pode usar qualquer outra tabela, exibição ou função com valor de tabela.  
  
Use **OPENJSON** para importar dados JSON em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou converter dados JSON em formato relacional para um aplicativo ou serviço que não pode consumir JSON diretamente.  
  
> [!NOTE]  
>  O **OPENJSON** função está disponível somente no nível de compatibilidade 130 ou superior. Se o nível de compatibilidade do banco de dados for inferior a 130, o SQL Server não poderá localizar e executar a função **OPENJSON**. Outras funções JSON estão disponíveis em todos os níveis de compatibilidade.
> 
> É possível verificar o nível de compatibilidade na exibição `sys.databases` ou nas propriedades do banco de dados. Você pode alterar o nível de compatibilidade do banco de dados com o seguinte comando:  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>   
> Nível de compatibilidade 120 pode ser a padrão até mesmo em um novo banco de dados SQL.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico")[convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

O **OPENJSON** função com valor de tabela analisa o *jsonExpression* fornecido como o primeiro argumento e retorna um ou mais linhas que contêm dados dos objetos de JSON na expressão. *jsonExpression* pode conter subobjetos aninhados. Se você quiser analisar um Subobjeto do *jsonExpression*, você pode especificar um **caminho** parâmetro para o objeto de subsistema de JSON.

### <a name="openjson"></a>openjson

![Sintaxe para OPENJSON TVF](../../relational-databases/json/media/openjson-syntax.png "sintaxe OPENJSON")  

Por padrão, o **OPENJSON** função com valor de tabela retorna três colunas, que contém o nome da chave, o valor e o tipo de cada par de {chave: valor} encontrado *jsonExpression*. Como alternativa, você pode especificar explicitamente o esquema do resultado definido que **OPENJSON** retorna fornecendo *with_clause*.
  
### <a name="withclause"></a>with_clause
  
![Sintaxe com cláusula em OPENJSON TVF](../../relational-databases/json/media/openjson-shema-syntax.png "OPENJSON com sintaxe")

*with_clause* contém uma lista de colunas com seus tipos de **OPENJSON** para retornar. Por padrão, **OPENJSON** faz a correspondência de chaves em *jsonExpression* com os nomes de coluna na *with_clause* (nesse caso, as chaves de correspondências implica que diferencia maiusculas de minúsculas). Se um nome de coluna não coincide com um nome de chave, você pode fornecer um recurso opcional *column_path*, que é um [expressão de caminho JSON](../../relational-databases/json/json-path-expressions-sql-server.md) que faz referência a uma chave dentro de *jsonExpression*. 

## <a name="arguments"></a>Argumentos  
### <a name="jsonexpression"></a>*jsonExpression*  
Uma expressão de caractere Unicode que contém o texto JSON.  
  
OPENJSON itera sobre os elementos da matriz ou as propriedades do objeto na expressão de JSON e retorna uma linha para cada elemento ou propriedade. O exemplo a seguir retorna cada propriedade do objeto fornecido como *jsonExpression*:  
  
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
|IntValue|Doe|2|  
|trueValue|true|3|  
|falseValue|false|3|  
|nullValue|NULL|0|  
|ArrayValue|["a", "r", "r", "y",""]|4|  
|ObjectValue|{"obj": "ect"}|5|  

### <a name="path"></a>*caminho*  
É uma expressão de caminho JSON opcional que faz referência a um objeto ou uma matriz em *jsonExpression*. **OPENJSON** buscas em texto JSON na posição especificada e analisa apenas o fragmento referenciado. Para obter mais informações, consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).

Em [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e em [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *caminho*.
  
O exemplo a seguir retorna um objeto aninhado, especificando o *caminho*:  

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

A comparação usada para corresponder as etapas do demarcador com as propriedades da expressão JSON é diferencia maiusculas de minúsculas e sem reconhecimento de agrupamento (ou seja, uma comparação BIN2). 

### <a name="withclause"></a>*with_clause*
Define explicitamente o esquema de saída para o **OPENJSON** função para retornar. Opcional *with_clause* pode conter os seguintes elementos:

*colName* é o nome da coluna de saída.  
  
Por padrão, **OPENJSON** usa o nome da coluna para corresponder a uma propriedade no texto JSON. Por exemplo, se você especificar a coluna *nome* no esquema, OPENJSON tenta preencher essa coluna com a propriedade "name" no texto JSON. Você pode substituir esse mapeamento padrão usando o *column_path* argumento.  
  
*tipo*  
É o tipo de dados da coluna de saída.  

> [!NOTE]
> Se você usar também o **AS JSON** opção, a coluna *tipo* devem ser `NVARCHAR(MAX)`.
  
*column_path*  
É o caminho JSON que especifica a propriedade a ser retornada na coluna especificada. Para obter mais informações, consulte a descrição do *caminho* parâmetro anteriormente neste tópico.  
  
Use *column_path* para substituir as regras de mapeamento padrão quando o nome de uma coluna de saída não corresponde ao nome da propriedade.  
  
A comparação usada para corresponder as etapas do demarcador com as propriedades da expressão JSON é diferencia maiusculas de minúsculas e sem reconhecimento de agrupamento (ou seja, uma comparação BIN2).  
  
Para obter mais informações sobre os caminhos, consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
*COMO JSON*  
Use o **AS JSON** opção em uma definição de coluna para especificar que a propriedade referenciada contém um objeto JSON interno ou uma matriz. Se você especificar o **AS JSON** opção, o tipo da coluna deve ser nvarchar (max).

-   Se você não especificar **AS JSON** para uma coluna, a função retorna um valor escalar (por exemplo, int, string, verdadeiro, FALSO) da propriedade JSON especificada no caminho especificado. Se o caminho representa um objeto ou uma matriz, e a propriedade não pode ser encontrada no caminho especificado, a função retornará um valor nula no modo incerto ou retornará um erro no modo estrito. Esse comportamento é semelhante ao comportamento do **JSON_VALUE** função.  
  
-   Se você especificar **AS JSON** para uma coluna, a função retorna um fragmento JSON da propriedade JSON especificada no caminho especificado. Se o caminho representa um valor escalar, e a propriedade não pode ser encontrada no caminho especificado, a função retornará um valor nula no modo incerto ou retornará um erro no modo estrito. Esse comportamento é semelhante ao comportamento do **JSON_QUERY** função.  
  
> [!NOTE]  
> Se você quiser retornar um fragmento JSON aninhado de uma propriedade JSON, você precisa fornecer o **AS JSON** sinalizador. Sem essa opção, se a propriedade não pode ser encontrada, OPENJSON retorna um valor nulo em vez da matriz ou objeto JSON referenciado ou retorna um erro de tempo de execução no modo estrito.  
  
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
  
|Número|Data|Cliente|Quantidade|Order|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|{"Number": "SO43659", "Data": "2011-05-31T00:00:00"}|  
|SO43661|2011-06-01T00:00:00|AW73565|3|{"Number": "SO43661", "Data": "2011-06-01T00:00:00"}|  
  

## <a name="return-value"></a>Valor de retorno  
As colunas que a função OPENJSON retorna dependem da opção WITH.  
  
1. Quando você chama o OPENJSON com o esquema padrão - ou seja, quando você não especificar um esquema explícito na cláusula WITH - a função retorna uma tabela com as seguintes colunas:  
    1.  **Chave**. Um valor nvarchar (4000) que contém o nome da propriedade especificada ou o índice do elemento na matriz especificada. A coluna de chave tem um agrupamento BIN2.  
    2.  **Valor**. Um valor nvarchar (max) que contém o valor da propriedade. A coluna de valor herda seu agrupamento de *jsonExpression*.
    3.  **Tipo**. Um valor inteiro que contém o tipo do valor. O **tipo** coluna é retornada somente quando você usar OPENJSON com o esquema padrão. A coluna de tipo tem um dos seguintes valores:  
  
        |Valor da coluna de tipo|Tipo de dados JSON|  
        |------------------------------|--------------------|  
        |0|nulo|  
        |1|cadeia de caracteres|  
        |2|int|  
        |3|Verdadeiro/Falso|  
        |4|matriz|  
        |5|objeto|  
  
     Somente propriedades de primeiro nível são retornadas. A instrução falhará se o texto JSON não está formatado corretamente.  

2. Quando você chamar OPENJSON e você especificar um esquema explícito na cláusula WITH, a função retorna uma tabela com o esquema definido na cláusula WITH.  

## <a name="remarks"></a>Comentários  

*json_path* usado no segundo argumento de **OPENJSON** ou *with_clause* pode iniciar com o **lax** ou **estrito** palavra-chave.

-   Em **lax** modo, **OPENJSON** ação não gerará um erro se o objeto ou o valor no caminho especificado não pode ser encontrado. Se o caminho não pode ser encontrado, **OPENJSON** retorna um conjunto de resultados vazio ou um valor NULL.
-   Em **estrito**, modo **OPENJSON** retorna um erro se o caminho não pode ser encontrado.

Alguns dos exemplos nessa página especificar explicitamente o modo path, lax ou strict. O modo path é opcional. Se você não especificar explicitamente o modo de path, o modo incerto é o padrão. Para obter mais informações sobre o modo path e expressões de caminho, consulte [expressões de caminho JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).    

Nomes de coluna nas *with_clause* são correspondidas com as chaves no texto JSON. Se você especificar o nome da coluna `[Address.Country]`, ele é correspondido com a chave `Address.Country`. Se você quiser fazer referência a uma chave aninhada `Country` dentro do objeto `Address`, você deve especificar o caminho `$.Address.Country` no caminho da coluna.

*json_path* podem conter chaves com caracteres alfanuméricos. Ignorar o nome de chave em *json_path* com aspas duplas, se você tiver caracteres especiais em chaves. Por exemplo, `$."my key $1".regularKey."key with . dot"` corresponde ao valor 1 no seguinte texto JSON:

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
O exemplo a seguir fornece uma lista de identificadores como uma matriz JSON dos números. A consulta converte a matriz JSON em uma tabela de identificadores e filtra todos os produtos com as ids especificadas.  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
Esta consulta é equivalente ao exemplo a seguir. No entanto, no exemplo a seguir, você precisa inserir números na consulta em vez de transmiti-los como parâmetros.  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>Exemplo 2 - propriedades de mesclagem de dois objetos JSON  
O exemplo a seguir seleciona uma união de todas as propriedades de dois objetos JSON. Os dois objetos têm uma duplicata *nome* propriedade. O exemplo usa o valor da chave para excluir a linha duplicada dos resultados.  
  
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
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>Exemplo 3 - linhas de junção com dados JSON armazenados em células de tabela usando CROSS APPLY  
No exemplo a seguir, o `SalesOrderHeader` tabela tem um `SalesReason` coluna de texto que contém uma matriz de `SalesOrderReasons` no formato JSON. O `SalesOrderReasons` objetos contêm propriedades como *qualidade* e *fabricante*. O exemplo cria um relatório que une cada linha da ordem de venda aos motivos de vendas relacionados. O operador OPENJSON expande a matriz JSON de motivos de vendas como se os motivos estivessem armazenados em uma tabela filho separada. Em seguida, o operador CROSS APPLY une cada linha da ordem de venda às linhas retornadas pela função com valor de tabela OPENJSON.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> Quando é necessário expandir matrizes JSON armazenado em campos individuais e associá-las com suas linhas pai, você normalmente usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] operador CROSS APPLY. Para obter mais informações sobre CROSS APPLY, consulte [FROM &#40; Transact-SQL &#41; ](../../t-sql/queries/from-transact-sql.md).  
  
A mesma consulta pode ser reescrita usando `OPENJSON` com um esquema definido explicitamente de linhas a serem retornadas:  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
Neste exemplo, o `$` caminho faz referência a cada elemento da matriz. Se você quiser converter explicitamente o valor retornado, você pode usar esse tipo de consulta.  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>Exemplo 4 - combinar linhas relacionais e elementos JSON com CROSS APPLY  
A consulta a seguir combina linhas relacionais e elementos JSON nos resultados mostrados na tabela a seguir.  
  
```sql  
SELECT store.title, location.street, location.lat, location.long  
FROM store  
CROSS APPLY OPENJSON(store.jsonCol, 'lax $.location')   
     WITH (street varchar(500) ,  postcode  varchar(500) '$.postcode' ,  
     lon int '$.geo.longitude', lat int '$.geo.latitude')  
     AS location
```  
  
**Resultados**  
  
|title|Rua|CEP|LON|LAT|  
|-----------|------------|--------------|---------|---------|  
|Mercados de alimentos inteira|Forma de Redmond 17991|WA 98052|47.666124|-122.10155|  
|Sears|148th Ave NE|WA 98052|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>Exemplo 5 - importar dados JSON no SQL Server  
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
        dateOfBirth datetime2, spouse nvarchar(50)
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões de caminho JSON &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Converter dados JSON em linhas e colunas com OPENJSON &#40; SQL Server &#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [Usar OPENJSON com o esquema padrão &#40; SQL Server &#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [Usar OPENJSON com esquema explícito &#40; SQL Server &#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
  

