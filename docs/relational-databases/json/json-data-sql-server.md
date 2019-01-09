---
title: Trabalhar com os dados JSON no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/19/2018
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: quickstart
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b25ee3d20432b5cba03fb745f8d95e51771619ec
ms.sourcegitcommit: 0330cbd1490b63e88334a9f9e421f4bd31a6083f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52886931"
---
# <a name="json-data-in-sql-server"></a>Dados JSON no SQL Server
[!INCLUDE[appliesto-ss2016-asdb-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [Ajude a aprimorar os documentos do SQL Server!](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

JSON é um formato popular de dados textuais usado para troca de dados em aplicativos Web e móveis modernos. JSON também é usado para armazenar dados não estruturados em arquivos de log ou em bancos de dados NoSQL, como o Microsoft Azure Cosmos DB. Muitos serviços Web REST retornam resultados formatados como texto JSON ou aceitam dados formatados como JSON. Por exemplo, a maioria dos serviços do Azure, como o Azure Search, o Armazenamento do Azure e o Azure Cosmos DB, tem pontos de extremidade REST que retornam ou consomem JSON. JSON também é o principal formato para troca de dados entre páginas da Web e servidores Web usando chamadas AJAX. 

As funções JSON no SQL Server permitem combinar NoSQL e conceitos relacionais no mesmo banco de dados. Agora você pode combinar colunas relacionais clássicas com colunas que contêm documentos formatados como texto JSON na mesma tabela, analisar e importar documentos JSON em estruturas relacionais ou formatar dados relacionais em texto JSON. No vídeo a seguir, você verá como as funções JSON conectam conceitos relacionais e NoSQL no SQL Server e no Banco de Dados SQL do Azure:

*JSON é uma ponte entre o NoSQL e mundos relacionais*
> [!VIDEO https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds/player]
 
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
 
Usando funções internas e operadores do SQL Server, é possível realizar as ações a seguir com o texto JSON: 
 
- Analise texto JSON e leia ou modifique os valores.  
- Transforme matrizes de objetos JSON em formato de tabela.  
- Executar uma consulta Transact-SQL nos objetos JSON convertidos.  
- Formate os resultados de consultas Transact-SQL em formato JSON.  
  
![Visão geral do suporte interno a JSON](../../relational-databases/json/media/jsonslides1overview.png "Visão geral do suporte interno a JSON")  
  
## <a name="key-json-capabilities-of-sql-server-and-sql-database"></a>Principais funcionalidades do JSON no SQL Server e no Banco de dados SQL
As seções a seguir discutem as principais funcionalidades fornecidas pelo SQL Server com seu suporte interno ao JSON. No vídeo a seguir, você verá como usar os operadores e funções JSON:

*SQL Server 2016 e suporte para JSON*
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support/player]

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>Extrair valores do texto JSON e usá-los em consultas
Caso haja texto JSON armazenado em tabelas de banco de dados, é possível ler ou modificar valores no texto JSON usando as seguintes funções internas:  
    
-   [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md) testa se uma cadeia de caracteres contém um JSON válido.
-   [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md) extrai um valor escalar de uma cadeia de caracteres JSON.
-   [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md) extrai um objeto ou uma matriz de uma cadeia de caracteres JSON.
-   [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md) altera um valor em uma cadeia de caracteres JSON.


**Exemplo**
  
No exemplo a seguir, a consulta usa tanto dados JSON quanto relacionais (armazenados em uma coluna chamada `jsonCol`) de uma tabela:  
  
```sql  
SELECT Name,Surname,
 JSON_VALUE(jsonCol,'$.info.address.PostCode') AS PostCode,
 JSON_VALUE(jsonCol,'$.info.address."Address Line 1"')+' '
  +JSON_VALUE(jsonCol,'$.info.address."Address Line 2"') AS Address,
 JSON_QUERY(jsonCol,'$.info.skills') AS Skills
FROM People
WHERE ISJSON(jsonCol)>0
 AND JSON_VALUE(jsonCol,'$.info.address.Town')='Belgrade'
 AND Status='Active'
ORDER BY JSON_VALUE(jsonCol,'$.info.address.PostCode')
```  
  
Os aplicativos e ferramentas não percebem nenhuma diferença entre os valores extraídos de colunas de tabela escalar e os valores extraídos da coluna JSON. Você pode usar valores do texto JSON em qualquer parte de uma consulta Transact-SQL (incluindo, cláusulas WHERE, ORDER BY ou GROUP BY, agregações de janela e assim por diante). As funções JSON usam sintaxe semelhante a do JavaScript para fazer referência a valores no texto JSON.

Para obter mais informações, consulte [Validar, consultar e alterar dados JSON com funções internas (SQL Server)](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md), [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)e [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md).  
  
### <a name="change-json-values"></a>Alterar os valores JSON
Se precisar modificar partes do texto JSON, use a função [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md) para atualizar o valor de uma propriedade em uma cadeia de caracteres JSON e retornar a cadeia de caracteres JSON atualizada. O exemplo a seguir atualiza o valor de uma propriedade em uma variável que contém JSON:  
  
```sql  
DECLARE @json NVARCHAR(MAX);
SET @json = '{"info":{"address":[{"town":"Belgrade"},{"town":"Paris"},{"town":"Madrid"}]}}';
SET @json = JSON_MODIFY(@json,'$.info.address[1].town','London');
SELECT modifiedJson = @json;
```  
**Resultados**  

|modifiedJson|  
|--------|  
|{"info":{"address":[{"town":"Belgrade"},{"town":"London"},{"town":"Madrid"}]}|  
  
### <a name="convert-json-collections-to-a-rowset"></a>Converter coleções JSON em um conjunto de linhas
Você não precisa de uma linguagem de consulta personalizada para consultar o JSON no SQL Server. Para consultar dados JSON, é possível usar o T-SQL padrão. Se precisar criar uma consulta ou um relatório sobre dados JSON, você poderá converter facilmente os dados JSON em linhas e colunas chamando a função de conjunto de linhas **OPENJSON**. Para obter mais informações, consulte [Converter dados JSON em linhas e colunas com OPENJSON (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).  
  
O seguinte exemplo chama **OPENJSON** e transforma a matriz de objetos armazenados na variável `@json` em um conjunto de linhas que pode ser consultado com uma instrução SQL **SELECT** padrão:  
  
```sql  
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
  
**OPENJSON** transforma a matriz de objetos JSON em uma tabela, na qual cada objeto é representado como uma linha e os pares chave/valor são retornados como células. O resultado segue as seguintes regras:
- **OPENJSON** converte valores JSON nos tipos especificados na cláusula **WITH**.
- **OPENJSON** pode lidar com pares simples de chave:valor e objetos aninhados hierarquicamente organizados.
- Você não precisa retornar todos os campos contidos no texto JSON.
- Se não houver valores JSON, o **OPENJSON** retornará valores NULL.
- Opcionalmente, é possível especificar um caminho após a especificação de tipo para referenciar uma propriedade aninhada ou uma propriedade por outro nome.
- O prefixo **strict** opcional no caminho especifica que os valores para as propriedades especificadas devem existir no texto JSON.

Para obter mais informações, consulte [Converter dados JSON em linhas e colunas com OPENJSON (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) e [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md).  

Os documentos JSON podem ter subelementos e dados hierárquicos que não podem ser mapeados diretamente nas colunas relacionais padrão. Nesse caso, você poderá mesclar a hierarquia JSON unindo a entidade pai às submatrizes.

No exemplo a seguir, o segundo objeto na matriz tem uma submatriz que representa as habilidades da pessoa. Cada subobjeto pode ser analisado usando uma chamada adicional à função `OPENJSON`: 

```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =  
N'[  
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith", "skills": ["SQL", "C#", "Azure"] }, "dob": "2005-11-04T12:00:00" }  
 ]'  
   
SELECT *  
FROM OPENJSON(@json)  
  WITH (id int 'strict $.id',  
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',  
        age int, dateOfBirth datetime2 '$.dob',
    skills nvarchar(max) '$.info.skills' as json) 
    outer apply openjson( skills ) 
                     with ( skill nvarchar(8) '$' )
```  
A matriz **skills** é retornada no primeiro `OPENJSON` como um fragmento de texto JSON original e passada para outra função `OPENJSON` usando o operador `APPLY`. A segunda função `OPENJSON` analisará a matriz JSON e retornará valores de cadeia de caracteres como um único conjunto de linhas de coluna que será associado ao resultado do primeiro `OPENJSON`. O resultado dessa consulta é mostrado na seguinte tabela:

**Resultados**  
  
|id|firstName|lastName|age|dateOfBirth|skill|  
|--------|---------------|--------------|---------|-----------------|----------|  
|2|John|Smith|25|||  
|5|Jane|Smith||2005-11-04T12:00:00|SQL| 
|5|Jane|Smith||2005-11-04T12:00:00|C#|
|5|Jane|Smith||2005-11-04T12:00:00|Azure|

`OUTER APPLY OPENJSON` unirá a entidade de primeiro nível à submatriz e retornará um conjunto de resultados mesclado. Devido ao uso de JOIN, a segunda linha será repetida para cada habilidade.

### <a name="convert-sql-server-data-to-json-or-export-json"></a>Converter dados do SQL Server em JSON ou exportar JSON
Formate dados do SQL Server ou os resultados de consultas SQL como JSON, adicionando a cláusula **FOR JSON** a uma instrução **SELECT** . Use **FOR JSON** para delegar a formatação da saída JSON do seu aplicativo cliente ao SQL Server. Para obter mais informações, consulte [Formatar Resultados da Pesquisa como JSON para FOR JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
O exemplo a seguir usa o modo PATH com a cláusula **FOR JSON**:  
  
```sql  
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
  
Para obter mais informações, consulte [Formatar Resultados da Pesquisa como JSON para FOR JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) e [Cláusula FOR (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md).  

## <a name="use-cases-for-json-data-in-sql-server"></a>Usar casos para dados JSON no SQL Server

O suporte a JSON no SQL Server e no Banco de Dados SQL do Azure permite combinar conceitos relacionais e NoSQL. É possível transformar facilmente dados relacionais em semiestruturados e vice-versa. No entanto, o JSON não é uma substituição para modelos relacionais existentes. Aqui estão alguns casos de uso específicos que se beneficiam do suporte a JSON no SQL Server e no Banco de Dados SQL.

### <a name="simplify-complex-data-models"></a>Simplificar modelos de dados complexos

Considere a desnormalização de seu modelo de dados com campos JSON em vez de várias tabelas filho.

### <a name="store-retail-and-e-commerce-data"></a>Armazenar dados de varejo e de comércio eletrônico

Armazene informações sobre produtos com uma ampla gama de atributos de variável em um modelo desnormalizado para obter flexibilidade.

### <a name="process-log-and-telemetry-data"></a>Processar dados de log e de telemetria

Carregue, consulte e analise dados de log armazenados como arquivos JSON com todos os recursos da linguagem Transact-SQL.

### <a name="store-semi-structured-iot-data"></a>Armazenar dados semiestruturados de IoT

Quando precisar de análise em tempo real de dados de IoT, carregue os dados de entrada diretamente no banco de dados, em vez de prepará-los em um local de armazenamento.

### <a name="simplify-rest-api-development"></a>Simplificar o desenvolvimento da API REST

Transforme dados relacionais do seu banco de dados facilmente no formato JSON usado pelas APIs REST compatíveis com seu site da Web.

## <a name="combine-relational-and-json-data"></a>Combinar dados relacionais e dados JSON
O SQL Server fornece um modelo híbrido para armazenar e processar dados relacionais e JSON usando linguagem padrão Transact-SQL. Você pode organizar coleções de seus documentos JSON em tabelas, estabelecer relações entre elas, combinar colunas escalares fortemente tipadas armazenadas em tabelas com pares chave/valor flexíveis armazenadas em colunas JSON e consultar valores escalares e JSON em uma ou várias tabelas usando o Transact-SQL completo.
 
O texto JSON é armazenado em colunas varchar ou nvarchar e é indexado como texto sem formatação. Qualquer componente ou recurso do SQL Server que dá suporte a texto dá suporte a JSON e, portanto, quase não há restrições na interação entre JSON e outros recursos do SQL Server. Você pode armazenar o JSON na Memória ou em Tabelas temporais, aplicar predicados de Segurança em nível de linha em texto JSON e assim por diante.

Se você tiver cargas de trabalhos JSON puras nas quais queira usar uma linguagem de consulta que seja personalizada para o processamento de documentos JSON, considere o Microsoft Azure [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).  
  
Veja alguns casos de uso que mostram como é possível usar o suporte JSON interno no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="store-and-index-json-data-in-sql-server"></a>Armazenar e indexar dados JSON no SQL Server

JSON é um formato textual para que documentos JSON possam ser armazenados em colunas `NVARCHAR` no Banco de Dados SQL. Como o tipo `NVARCHAR` dá suporte a todos os subsistemas do SQL Server, é possível colocar documentos JSON em tabelas com índices **CLUSTERED COLUMNSTORE**, tabelas **otimizadas para memória** ou arquivos externos que podem ser lidos usando OPENROWSET ou o PolyBase.

Para saber mais sobre as opções de armazenamento, indexação e otimização dos dados JSON no SQL Server, consulte os seguintes artigos:
-   [Armazenar documentos JSON no SQL Server ou no Banco de Dados SQL](store-json-documents-in-sql-tables.md)
-   [Indexar dados JSON](index-json-data.md)
-   [Otimizar o processamento JSON com o OLTP in-memory](optimize-json-processing-with-in-memory-oltp.md)

### <a name="load-json-files-into-sql-server"></a>Carregar arquivos JSON no SQL Server  

É possível formatar informações armazenadas em arquivos como JSON padrão ou JSON delimitado por linha. O SQL Server pode importar o conteúdo de arquivos JSON, analisá-lo usando as funções **OPENJSON** ou **JSON_VALUE** e carregá-lo em tabelas.  
  
-   Se seus documentos JSON estiverem armazenados em arquivos locais, em unidades de rede compartilhadas ou em locais de Arquivos do Azure que podem ser acessados pelo SQL Server, você poderá usar a importação em massa para carregar os dados JSON no SQL Server.
  
-   Se os arquivos delimitados por linha estiverem armazenados no sistema de arquivos do Hadoop ou no Armazenamento de Blobs do Azure, você poderá usar o PolyBase para carregar texto JSON, analisá-lo no código Transact-SQL e carregá-lo em tabelas.  

### <a name="import-json-data-into-sql-server-tables"></a>Importar dados JSON em tabelas do SQL Server  
Se precisar carregar dados JSON de um serviço externo no SQL Server, você poderá usar **OPENJSON** para importar os dados para o SQL Server em vez de analisá-los na camada de aplicativo.  
  
```sql  
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
  
Você pode fornecer o conteúdo da variável JSON por um serviço REST externo, enviado como um parâmetro de uma estrutura JavaScript do lado do cliente ou carregado de arquivos externos. Você pode inserir, atualizar ou mesclar facilmente resultados de texto JSON em uma tabela do SQL Server.

## <a name="analyze-json-data-with-sql-queries"></a>Analisar dados JSON com consultas SQL  
Se precisar filtrar ou agregar dados JSON para fins de relatório, você poderá usar **OPENJSON** para transformar o JSON em um formato relacional. Você pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] padrão e funções internas para preparar os relatórios.  
  
```sql  
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
  
Você pode usar colunas de tabela padrão e valores do texto JSON na mesma consulta. É possível adicionar índices na expressão `JSON_VALUE(Tab.json, '$.Status')` para melhorar o desempenho da consulta. Para obter mais informações, consulte [Indexar dados JSON](../../relational-databases/json/index-json-data.md).
 
## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>Retornar dados de uma tabela do SQL Server formatada como JSON  
Se tiver um serviço Web que usa dados da camada do banco de dados e os retorna no formato JSON ou se tiver estruturas ou bibliotecas JavaScript que aceitam dados formatados como JSON, você poderá formatar o resultado em JSON diretamente em uma consulta SQL. Em vez de escrever código ou incluir uma biblioteca para converter resultados da consulta de tabela e serializar objetos no formato JSON, você pode usar **FOR JSON** para delegar a formatação JSON ao SQL Server.  
  
Por exemplo, pode ser conveniente gerar uma saída JSON em conformidade com a especificação OData. O serviço Web espera uma solicitação e uma resposta no formato a seguir: 
  
-   Solicitação: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  
  
-   Resposta: `{"@odata.context":"https://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity","ProductID":1,"ProductName":"Chai"}`  
  
Essa URL do OData representa uma solicitação para as colunas ProductID e ProductName do produto com `id` 1. Você pode usar **FOR JSON** para formatar o resultado conforme esperado no SQL Server.  
  
```sql  
SELECT 'https://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity'
 AS '@odata.context',   
 ProductID, Name as ProductName   
FROM Production.Product  
WHERE ProductID = 1  
FOR JSON AUTO  
```  
  
A saída dessa consulta é um texto JSON que está em conformidade total com a especificação OData. A formatação e a saída são manipuladas pelo SQL Server. O SQL Server também pode formatar resultados de consulta em qualquer formato, como OData JSON ou GeoJSON.  
  
## <a name="test-drive-built-in-json-support-with-the-adventureworks-sample-database"></a>Faça o test drive do suporte interno para JSON com o banco de dados de exemplo AdventureWorks
Para obter o banco de dados de exemplo AdventureWorks, baixe pelo menos o arquivo de banco de dados e o arquivo de exemplos e scripts no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=49502). 
 
Após restaurar o banco de dados de exemplo para uma instância do SQL Server 2016, extraia o arquivo de exemplos e abra o arquivo *JSON Sample Queries procedures views and indexes.sql* da pasta JSON. Execute os scripts nesse arquivo para reformatar alguns dados existentes como dados JSON, testar relatórios e consultas de exemplo em dados JSON, indexar os dados JSON e importar e exportar JSON.  
  
Veja o que você pode fazer com os scripts incluídos no arquivo:  
  
* Desnormalize o esquema existente para criar colunas de dados JSON.
  
    * Armazene informações de SalesReasons, SalesOrderDetails, SalesPerson, Customer e outras tabelas que contenham informações relacionadas a ordens de venda nas colunas JSON da tabela SalesOrder_json.  
  
    * Armazene informações das tabelas EmailAddresses/PersonPhone na tabela Person_json como matrizes de objetos JSON.  
  
* Crie procedimentos e exibições que consultem dados JSON.  
  
* Indexar dados JSON. Crie índices em propriedades JSON e índices de texto completo.  
  
* Importar e exportar JSON. Crie e execute procedimentos que exportem o conteúdo das tabelas Person e SalesOrder como resultados JSON, e importe e atualize as tabelas Person e SalesOrder usando a entrada JSON.  
  
* Executar exemplos de consulta. Execute algumas consultas que chamem os procedimentos armazenados e exibições criados nas etapas 2 e 4.  
  
* Limpar scripts. Não execute essa parte se quiser manter os procedimentos armazenados e exibições criados nas etapas 2 e 4.  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual do suporte interno a JSON no SQL Server e no Banco de Dados SQL do Azure, assista ao vídeo a seguir:

*Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure*
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database/player]

*Building REST API with SQL Server using JSON functions* (Criando a API REST com o SQL Server usando funções JSON)
> [!VIDEO https://www.youtube.com/embed/0m6GXF3-5WI]

### <a name="reference-articles"></a>Artigos de referência  
  
-   [Cláusula FOR (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md) (FOR JSON)  
-   [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
-   [Funções JSON (Transact-SQL)](../../t-sql/functions/json-functions-transact-sql.md)  
    -   [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)  
    -   [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)  
    -   [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)  
    -   [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)  
