---
title: Converter dados JSON em linhas e colunas com OPENJSON (SQL Server) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea85d2dff3afe1b5e5b56117255576f8d0ae2180
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="convert-json-data-to-rows-and-columns-with-openjson-sql-server"></a>Converter dados JSON em linhas e colunas com OPENJSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

A função de conjunto de linhas **OPENJSON** converte o texto JSON em um conjunto de linhas e colunas. Use **OPENJSON** para executar consultas SQL em coleções JSON ou para importar texto JSON em tabelas do SQL Server.  
  
 A função **OPENJSON** obtém um único objeto JSON ou uma coleção de objetos JSON e transforma-os em uma ou mais linhas. Por padrão, a função **OPENJSON** retorna o seguinte.
-   De um objeto JSON, todos os pares chave:valor que ele localiza no primeiro nível.
-   De uma matriz JSON, todos os elementos da matriz com seus índices.  
  
Opcionalmente, adicione uma cláusula **WITH** para especificar o esquema das linhas que a função **OPENJSON** retorna. Esse esquema explícito define a estrutura da saída.  
  
## <a name="use-openjson-without-an-explicit-schema-for-the-output"></a>Use OPENJSON sem um esquema explícito para a saída
Quando você usa a função **OPENJSON** sem fornecer um esquema explícito para os resultados, ou seja, sem uma cláusula **WITH** após OPENJSON, a função retorna uma tabela com as três colunas a seguir.
1.  O nome da propriedade no objeto de entrada (ou o índice do elemento na matriz de entrada).
2.  O valor da propriedade ou o elemento da matriz.
3.  O tipo (por exemplo, cadeia de caracteres, número, booliano, matriz ou objeto).

Cada propriedade do objeto JSON ou cada elemento da matriz é retornado como uma linha separada.  

Aqui está um exemplo rápido que usa **OPENJSON** com o esquema padrão e retorna uma linha para cada propriedade do objeto JSON.  
 
**Exemplo**
```tsql  
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

SELECT *
FROM OPENJSON(@json);
```  
  
**Resultados**  
  
|chave|value|tipo|  
|---------|-----------|----------|  
|name|John|1|  
|sobrenome|Doe|1|  
|idade|45|2|  
|habilidades|["SQL","C#","MVC"]|4|

### <a name="more-info"></a>Obter mais informações

Para obter mais informações e exemplos, consulte [Usar OPENJSON com o esquema padrão &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md).

Para sintaxe e uso, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md). 

    
## <a name="use-openjson-with-an-explicit-schema-for-the-output"></a>Usar OPENJSON com um esquema explícito para a saída
Quando você especificar um esquema para os resultados usando a cláusula **WITH** da função **OPENJSON**, a função retornará uma tabela com apenas as colunas que você definir na cláusula **WITH**. Na cláusula **WITH**, especifique uma coluna de saída do conjunto, seus tipos e os caminhos das propriedades de origem do JSON para cada valor de saída. **OPENJSON** itera na matriz de objetos JSON, lê o valor no caminho especificado para cada coluna e converte o valor no tipo especificado.  

Aqui está um exemplo rápido que usa **OPENJSON** com um esquema para os resultados que você especifica explicitamente.  
  
**Exemplo**
  
```tsql  
DECLARE @json NVARCHAR(MAX)
SET @json =   
  N'[  
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
   
SELECT * FROM  
 OPENJSON ( @json )  
WITH (   
              Number   varchar(200) '$.Order.Number' ,  
              Date     datetime     '$.Order.Date',  
              Customer varchar(200) '$.AccountNumber',  
              Quantity int          '$.Item.Quantity'  
 ) 
```  
  
**Resultados**  
  
|Número|Data|Cliente|Quantidade|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
 Essa função retorna e formata os elementos de uma matriz JSON.  
  
-   Para cada elemento na matriz JSON, **OPENJSON** gera uma nova linha na tabela de saída. Os dois elementos na matriz JSON são convertidos em duas linhas na tabela retornada.  
  
-   Para cada coluna especificada usando a sintaxe `colName type json_path`, a função **OPENJSON** converte o valor encontrado em cada elemento da matriz do caminho especificado no tipo especificado e popula uma célula na tabela de saída. Neste exemplo, os valores para a coluna `Date` são tirados de cada objeto no caminho `$.Order.Date` e convertidos em valores de data/hora.  
  
Depois de transformar uma coleção de JSON em um conjunto de linhas com **OPENJSON**, você pode executar qualquer consulta SQL nos dados retornados ou inseri-los em uma tabela.  

### <a name="more-info"></a>Obter mais informações
Para obter mais informações e exemplos, consulte [Usar OPENJSON com o esquema explícito &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md).

Para sintaxe e uso, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).

## <a name="openjson-requires-compatibility-level-130"></a>O OPENJSON requer o nível de compatibilidade 130
A função **OPENJSON** está disponível somente no **nível de compatibilidade 130**. Se o nível de compatibilidade do banco de dados for inferior a 130, o SQL Server não poderá localizar e executar a função **OPENJSON** . Outras funções internas do JSON estão disponíveis em todos os níveis de compatibilidade. Você pode verificar o nível de compatibilidade na exibição sys.databases ou nas propriedades do banco de dados.

Você pode alterar um nível de compatibilidade do banco de dados usando o seguinte comando:   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-openjson-and-built-in-json-support-in-sql-server"></a>Saiba mais sobre o OPENJSON e o suporte interno a JSON no SQL Server  
 [Postagens no blog por Jovan Popovic, gerente de programas da Microsoft](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## <a name="see-also"></a>Consulte também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  

