---
title: Dados JSON (SQL Server) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3daaaa3dc2fb53344b009a5b3ab3d1cfbdd19350
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="json-data-sql-server"></a>Dados JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

JSON é um formato popular de dados textuais usado para a troca de dados em aplicativos Web modernos e móveis. O JSON também é usado para armazenar dados não estruturados em arquivos de log ou bancos de dados NoSQL, como o Banco de Dados de Documentos do Microsoft Azure. Muitos serviços Web REST retornam resultados formatados como texto JSON ou aceitam dados formatados como JSON. Por exemplo, a maioria dos serviços do Azure, como o Azure Search, o Armazenamento do Azure e o Azure DocumentDB, tem pontos de extremidade REST que retornam ou consomem JSON. O JSON também é o principal formato para troca de dados entre páginas da Web e servidores Web usando chamadas AJAX.  
  
 Este é um texto JSON de exemplo:  
  
```json  
[{
    "name": "John",
    "skills": ["SQL", "C#", "Azure"]
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
  
 O SQL Server fornece funções internas e operadores que permitem realizar as ações a seguir com o texto JSON.  
  
-   Analise texto JSON e leia ou modifique os valores.  
  
-   Transforme matrizes de objetos JSON em formato de tabela.  
  
-   Executar uma consulta Transact-SQL nos objetos JSON convertidos.  
  
-   Formate os resultados de consultas Transact-SQL em formato JSON.  
  
 ![Visão geral do suporte interno a JSON](../../relational-databases/json/media/jsonslides1overview.png "Visão geral do suporte interno a JSON")  
  
## <a name="key-json-capabilities-of-sql-server"></a>Principais funcionalidades do JSON no SQL Server 
Veja mais informações sobre as principais funcionalidades fornecidas pelo SQL Server com seu suporte interno ao JSON.

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>Extrair valores do texto JSON e usá-los em consultas
Caso haja texto JSON armazenado em tabelas de banco de dados, você poderá usar funções internas para ler ou modificar valores no texto JSON.  
  
-   Usar a função **JSON_VALUE** para extrair um valor escalar de uma cadeia de caracteres JSON.
  
-   Usar **JSON_QUERY** para extrair um objeto ou uma matriz de uma cadeia de caracteres JSON.
  
-   Use a função **ISJSON** para testar se uma cadeia de caracteres contém JSON válido.

-   Usar a função **JSON_MODIFY** para alterar um valor em uma cadeia de caracteres JSON.

**Exemplo**
  
 No seguinte exemplo, a consulta usa dados relacionais e JSON (armazenados na coluna jsonCol) de uma tabela:  
  
```tsql  
SELECT Name,Surname,
 JSON_VALUE(jsonCol,'$.info.address.PostCode') AS PostCode,
 JSON_VALUE(jsonCol,'$.info.address."Address Line 1"')+' '
  +JSON_VALUE(jsonCol,'$.info.address."Address Line 2"') AS Address,
 JSON_QUERY(jsonCol,'$.info.skills') AS Skills
FROM PeopleCollection
WHERE ISJSON(jsonCol)>0
 AND JSON_VALUE(jsonCol,'$.info.address.Town')='Belgrade'
 AND Status='Active'
ORDER BY JSON_VALUE(jsonCol,'$.info.address.PostCode')
```  
  
 Os aplicativos e ferramentas não percebem nenhuma diferença entre os valores extraídos de colunas de tabela escalar e os valores extraídos da coluna JSON. Você pode usar valores do texto JSON em qualquer parte de uma consulta Transact-SQL (incluindo, cláusulas WHERE, ORDER BY ou GROUP BY, agregações de janela e assim por diante). As funções JSON usam sintaxe semelhante a do JavaScript para fazer referência a valores no texto JSON.

Para obter mais informações, veja [Validar, consultar e alterar dados JSON com funções internas &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md), [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)e [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
### <a name="change-json-values"></a>Alterar os valores JSON
Se você precisar modificar partes do texto JSON, poderá usar a função **JSON_MODIFY** para atualizar o valor de uma propriedade em uma cadeia de caracteres JSON e retornar a cadeia de caracteres JSON atualizada. O exemplo a seguir atualiza o valor de uma propriedade em uma variável que contém JSON.  
  
```tsql  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=JSON_MODIFY(@jsonInfo,'$.info.address[0].town','London') 
```  
  
### <a name="convert-json-collections-to-a-rowset"></a>Converter coleções JSON em um conjunto de linhas
Você não precisa de uma linguagem de consulta personalizada para consultar o JSON no SQL Server. Para consultar dados JSON, é possível usar o T-SQL padrão. Se você precisar criar uma consulta ou um relatório sobre dados JSON, poderá converter facilmente os dados JSON em linhas e colunas chamando a função de conjunto de linhas **OPENJSON**. Para obter mais informações, veja [Converter dados JSON em linhas e colunas com OPENJSON &#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).  
  
 O seguinte exemplo chama **OPENJSON** e transforma a matriz de objetos armazenados na variável `@json` em um conjunto de linhas que pode ser consultado com uma instrução SQL **SELECT** padrão:  
  
```tsql  
DECLARE @json NVARCHAR(MAX)
SET @json =  
N'[  
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith" }, "dob": "2005-11-04T12:00:00" }  
 ]'  
   
SELECT *  
FROM OPENJSON(@json)  
  WITH (id int 'strict $.id',  
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',  
        age int, dateOfBirth datetime2 '$.dob')  
```  
  
 **Resultados**  
  
|id|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|John|Smith|25||  
|5|Jane|Smith||2005-11-04T12:00:00|  
  
 **OPENJSON** transforma a matriz de objetos JSON em uma tabela, na qual cada objeto é representado como uma linha e os pares chave/valor são retornados como células. O resultado segue as regras abaixo.
-   **OPENJSON** converte valores JSON nos tipos especificados na cláusula **WITH**.
-   **OPENJSON** pode lidar com pares simples de chave:valor e objetos aninhados hierarquicamente organizados.
-   Você não precisa retornar todos os campos contidos no texto JSON.
-   **OPENJSON** retornará valores NULL se não houver valores JSON.
-   Opcionalmente, é possível especificar um caminho após a especificação de tipo para referenciar uma propriedade aninhada ou uma propriedade por outro nome.
-   O prefixo **strict** opcional no caminho especifica que os valores para as propriedades especificadas devem existir no texto JSON.

Para obter mais informações, veja [Converter dados JSON em linhas e colunas com OPENJSON &#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) e [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
### <a name="convert-sql-server-data-to-json-or-export-json"></a>Converter dados do SQL Server em JSON ou exportar JSON
Formate dados do SQL Server ou os resultados de consultas SQL como JSON, adicionando a cláusula **FOR JSON** a uma instrução **SELECT** . Use FOR JSON para delegar a formatação da saída JSON do seu aplicativo cliente ao SQL Server. Para obter mais informações, veja [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 O exemplo a seguir usa o modo PATH com a cláusula FOR JSON.  
  
```tsql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth as dob  
FROM People  
FOR JSON PATH  
```  
  
O **FOR JSON** formata os resultados do SQL como texto JSON, que pode ser fornecido a qualquer aplicativo que entenda JSON. A opção PATH usa aliases separados por ponto na cláusula SELECT para aninhar objetos nos resultados da consulta.  
  
 **Resultados**  
  
```json  
[{
    "id": 2,
    "info": {
        "name": "John",
        "surname": "Smith"
    },
    "age": 25
}, {
    "id": 5,
    "info": {
        "name": "Jane",
        "surname": "Smith"
    },
    "dob": "2005-11-04T12:00:00"
}] 
```  
  
 Para obter mais informações, veja [Formatar resultados da consulta como JSON com FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) e [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="combine-relational-and-json-data"></a>Combinar dados relacionais e dados JSON
 O SQL Server fornece um modelo híbrido para armazenar e processar dados relacionais e JSON usando linguagem padrão Transact-SQL. Você pode organizar coleções de seus documentos JSON em tabelas, estabelecer relações entre elas, combinar colunas escalares fortemente tipadas armazenadas em tabelas com pares chave/valor flexíveis armazenadas em colunas JSON e consultar valores escalares e JSON em uma ou várias tabelas usando o Transact-SQL completo.
 
Geralmente, o texto JSON é armazenado em colunas varchar ou nvarchar e é indexado como texto sem formatação. Qualquer componente ou recurso do SQL Server que dá suporte a texto dá suporte a JSON e, portanto, quase não há restrições na interação entre JSON e outros recursos do SQL Server. Você pode armazenar o JSON na Memória ou em Tabelas temporais, aplicar predicados de Segurança em nível de linha em texto JSON e assim por diante.

Se houver cargas de trabalhos JSON puras, em que você queira usar uma linguagem de consulta que seja personalizada para processamento de documentos JSON, considere o [Banco de Dados de Documentos](https://azure.microsoft.com/services/documentdb/)do Microsoft Azure.  
  
 Veja alguns casos de uso que mostram como é possível usar o suporte JSON interno no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>Retornar dados de uma tabela do SQL Server formatada como JSON  
 Se você tiver um serviço Web que usa dados da camada do banco de dados e os retorna no formato JSON ou estruturas ou bibliotecas JavaScript que aceitam dados formatados como JSON, poderá formatar o resultado em JSON diretamente em uma consulta SQL. Em vez de escrever código ou incluir uma biblioteca para converter resultados da consulta de tabela e serializar objetos no formato JSON, você pode usar FOR JSON para delegar a formatação JSON ao SQL Server.  
  
 Por exemplo, pode ser conveniente gerar uma saída JSON em conformidade com a especificação OData. O serviço Web espera uma solicitação e uma resposta no formato a seguir.  
  
-   Solicitação: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  
  
-   Resposta: `{"@odata.context":"http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity","ProductID":1,"ProductName":"Chai"}`  
  
 Essa URL do OData representa uma solicitação para as colunas ProductID e ProductName do produto com id 1. Você pode usar **FOR JSON** para formatar o resultado conforme esperado no SQL Server.  
  
```tsql  
SELECT 'http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity'
 AS '@odata.context',   
 ProductID, Name as ProductName   
FROM Production.Product  
WHERE ProductID = 1  
FOR JSON AUTO  
```  
  
O resultado dessa consulta é um texto JSON que está em conformidade total com a especificação OData. A formatação e a saída são manipuladas pelo SQL Server. O SQL Server também pode formatar os resultados da consulta em qualquer formato, como OData JSON ou GeoJSON. Para obter mais informações, consulte [Retornando dados espaciais no formato GeoJSON](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/returning-spatial-data-in-geojson-format-part-1).  
  
## <a name="analyze-json-data-with-sql-queries"></a>Analisar dados JSON com consultas SQL  
 Se você precisar filtrar ou agregar dados JSON para fins de relatório, poderá usar **OPENJSON** para transformar o JSON em um formato relacional. Em seguida, use [!INCLUDE[tsql](../../includes/tsql-md.md)] padrão e funções internas para preparar os relatórios.  
  
```tsql  
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date  
FROM   SalesOrderRecord AS Tab  
          CROSS APPLY  
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData  
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'  
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified  
```  
  
 Colunas de tabela padrão e valores do texto JSON podem ser usados na mesma consulta. É possível adicionar índices na expressão `JSON_VALUE(Tab.json, '$.Status')` para melhorar o desempenho da consulta. Para obter mais informações, veja [Indexar dados JSON](../../relational-databases/json/index-json-data.md).
  
## <a name="import-json-data-into-sql-server-tables"></a>Importar dados JSON em tabelas do SQL Server  
 Se você precisar carregar dados JSON de um serviço externo no SQL Server, poderá usar **OPENJSON** para importar os dados para o SQL Server em vez de analisá-los na camada de aplicativo.  
  
```tsql  
DECLARE @jsonVariable NVARCHAR(MAX)

SET @jsonVariable = N'[  
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
  
INSERT INTO SalesReport  
SELECT SalesOrderJsonData.*  
FROM OPENJSON (@jsonVariable, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData;  
```  
  
 O conteúdo da variável JSON pode ser fornecido por um serviço REST externo, enviado como um parâmetro de uma estrutura JavaScript do lado do cliente ou carregado de arquivos externos. Você pode inserir, atualizar ou mesclar resultados facilmente de texto JSON em tabela do SQL Server. Para obter mais informações sobre esse cenário, consulte as postagens de blog a seguir.
-   [Importing JSON data in SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/09/22/openjson-the-easiest-way-to-import-json-text-into-table/)
-   [Upsert JSON documents in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/03/upsert-json-documents-in-sql-server-2016)
-   [Loading GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/).  
  
## <a name="load-json-files-into-sql-server"></a>Carregar arquivos JSON no SQL Server  
 As informações armazenadas em arquivos podem ser formatadas como JSON padrão ou JSON Delimitado por Linha. O SQL Server pode importar o conteúdo de arquivos JSON, analisá-lo usando as funções **OPENJSON** ou **JSON_VALUE** e carregá-lo em tabelas.  
  
-   Se os documentos JSON estiverem armazenados em arquivos locais, em unidades de rede compartilhadas ou em locais de Armazenamento de Arquivos do Azure que pode ser acessado pelo SQL Server, você poderá usar a importação em massa para carregar os dados JSON no SQL Server. Para obter mais informações sobre esse cenário, confira [Importando arquivos JSON no SQL Server usando OPENROWSET (BULK)](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2015/10/07/importing-json-files-into-sql-server-using-openrowset-bulk.aspx).  
  
-   Se os arquivos delimitados por linha estiverem armazenados no sistema de arquivos do Hadoop ou no Armazenamento de Blobs do Azure, você poderá usar o PolyBase para carregar texto JSON, analisá-lo no código Transact-SQL e carregá-lo em tabelas.  
  
## <a name="test-drive-built-in-json-support"></a>Testar o suporte interno ao JSON  
 **Teste o suporte interno ao JSON com o banco de dado de exemplo AdventureWorks.** . Para obter o banco de dados de exemplo AdventureWorks, baixe pelo menos o arquivo de banco de dados e o arquivo de exemplos e scripts [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=49502). Depois de restaurar o banco de dados de exemplo para uma instância do SQL Server 2016, descompacte o arquivo de exemplos e abra o arquivo "JSON Sample Queries procedures views and indexes.sql" da pasta JSON. Execute os scripts nesse arquivo para reformatar alguns dados existentes como dados JSON, executar relatórios e consultas de exemplo em dados JSON, indexar os dados JSON e importar e exportar JSON.  
  
 Veja o que você pode fazer com os scripts incluídos no arquivo.  
  
1.  Desnormalize o esquema existente para criar colunas de dados JSON.  
  
    1.  Armazene informações de SalesReasons, SalesOrderDetails, SalesPerson, Customer e outras tabelas que contenham informações relacionadas a ordens de venda nas colunas JSON da tabela SalesOrder_json.  
  
    2.  Armazene informações das tabelas EmailAddresses/PersonPhone na tabela Person_json como matrizes de objetos JSON.  
  
2.  Crie procedimentos e exibições que consultem dados JSON.  
  
3.  Indexe dados JSON — crie índices em propriedades JSON e índices de texto completo.  
  
4.  Importe e exporte JSON — crie e execute procedimentos que exportem o conteúdo das tabelas Person e SalesOrder como resultados JSON, e importe e atualize as tabelas Person e SalesOrder usando a entrada JSON.  
  
5.  Execute exemplos de consulta — execute algumas consultas que chamem os procedimentos armazenados e exibições criados nas etapas 2 e 4.  
  
6.  Limpe scripts — não execute essa parte se quiser manter os procedimentos armazenados e exibições criados nas etapas 2 e 4.  
  
## <a name="learn-more-about-built-in-json-support"></a>Saiba mais sobre suporte interno ao JSON  
  
### <a name="topics-in-this-section"></a>Tópicos desta seção  
 [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
 Use a cláusula FOR JSON para delegar a formatação da saída JSON de aplicativos cliente ao SQL Server.  
  
 [Converter dados JSON em linhas e colunas com OPENJSON &#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)  
 Use OPENJSON para importar dados JSON no SQL Server ou para converter dados JSON em formato relacional para um aplicativo ou serviço que atualmente não possa consumir JSON diretamente, como o SQL Server Integration Services.  
  
 [Validar, consultar e alterar dados JSON com funções internas &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)  
 Use essas funções internas para validar texto JSON e extrair um valor escalar, um objeto ou uma matriz.  
  
 [Expressões de caminho JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
 Use uma expressão de caminho para especificar o texto JSON que você quer usar.  
  
 [Indexar dados JSON](../../relational-databases/json/index-json-data.md)  
 Use colunas computadas para criar índices habilitados para agrupamento sobre propriedades nos documentos JSON.  
  
[Solucionar problemas comuns com JSON no SQL Server](../../relational-databases/json/solve-common-issues-with-json-in-sql-server.md)  
 Encontre respostas para algumas perguntas comuns sobre o suporte interno a JSON no SQL Server.  
  
### <a name="microsoft-blog-posts"></a>Postagens no blog da Microsoft  
  
-   [Postagens no blog por Jovan Popovic, gerente de programas da Microsoft](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
### <a name="reference-topics"></a>Tópicos de referência  
  
-   [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md) (FOR JSON)  
  
-   [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
-   [Funções JSON &#40;Transact-SQL&#41;](../../t-sql/functions/json-functions-transact-sql.md)  
  
    -   [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)  
  
    -   [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)  
  
    -   [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
    -   [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)  
  
  

