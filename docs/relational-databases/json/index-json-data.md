---
description: Indexar dados JSON
title: Dados JSON do índice | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 81ba47199707e4f59094ec0070017610f61d3187
ms.sourcegitcommit: fb8724fb99c46ecf3a6d7b02a743af9b590402f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92439460"
---
# <a name="index-json-data"></a>Indexar dados JSON
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

No SQL Server e no Banco de Dados SQL, o JSON não é um tipo de dados interno e o SQL Server não tem índices JSON personalizados. No entanto, você pode otimizar suas consultas em documentos JSON usando índices padrão. 

Índices de bancos de dados melhoram o desempenho das operações de filtragem e classificação. Sem índices, o SQL Server precisa executar uma verificação de tabela completa sempre que você consultar dados.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indexar propriedades com colunas computadas  
Ao armazenar dados JSON no SQL Server, normalmente é útil filtrar ou classificar resultados de consulta pelas *propriedades* dos documentos JSON.  

### <a name="example"></a>Exemplo 
Neste exemplo, suponha que a tabela `SalesOrderHeader` do AdventureWorks tem uma coluna `Info` que contém várias informações em formato JSON sobre pedidos de venda. Por exemplo, ele contém informações sobre o cliente, vendedor, endereços de envio e de cobrança e assim por diante. Você deseja usar os valores da coluna `Info` para filtrar os pedidos de venda para um cliente.

### <a name="query-to-optimize"></a>Consulta para otimizar
Veja um exemplo do tipo de consulta que você deseja otimizar usando um índice.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>Índice de exemplo
Se você quiser acelerar seus filtros ou cláusulas `ORDER BY` em uma propriedade de um documento JSON, use os mesmos índices já usados em outras colunas. No entanto, não é possível fazer referências *diretamente* a propriedades em documentos JSON.
    
1.  Primeiro, você deve criar uma “coluna virtual” que retorna os valores que você deseja usar para filtragem.
2.  Em seguida, crie um índice na coluna virtual.  
  
O exemplo a seguir cria uma coluna computada que pode ser usada para indexação. Em seguida, ele cria um índice na nova coluna computada. Esse exemplo cria uma coluna que expõe o nome do cliente, que é armazenado no caminho `$.Customer.Name` nos dados JSON. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>Para obter mais informações sobre a coluna computada 
A coluna computada não é persistente. Ela é computada apenas quando o índice precisa ser recriado. Ela não ocupa espaço adicional na tabela.   
  
É importante criar a coluna computada com a mesma expressão que você planeja usar em suas consultas – neste exemplo, a expressão é `JSON_VALUE(Info, '$.Customer.Name')`.  
  
Não é preciso reescrever as consultas. Se você usar expressões com a função `JSON_VALUE`, como mostrado na consulta de exemplo anterior, o SQL Server observará que existe um equivalente da coluna computada com a mesma expressão e aplica um índice, se possível.

### <a name="execution-plan-for-this-example"></a>Plano de execução para este exemplo
Este é o plano de execução para a consulta no exemplo.  
  
![Captura de tela mostrando o plano de execução deste exemplo.](../../relational-databases/json/media/jsonindexblog1.png "Plano de execução")  
  
Em vez de uma verificação de tabela completa, o SQL Server usa uma busca de índice no índice não clusterizado e localiza as linhas que atendem às condições especificadas. Em seguida, ele usa uma pesquisa de chave na tabela `SalesOrderHeader` para buscar outras colunas referenciadas na consulta – neste exemplo, `SalesOrderNumber` e `OrderDate`.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>Otimizar ainda mais o índice com colunas incluídas
Se adicionar as colunas necessárias ao índice, você poderá evitar essa pesquisa adicional na tabela. É possível adicionar essas colunas como colunas incluídas padrão, conforme mostrado no exemplo a seguir, que expande o exemplo `CREATE INDEX` anterior.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
Nesse caso, o SQL Server não precisa ler dados adicionais da tabela `SalesOrderHeader`, pois tudo que ele precisa está incluído no índice JSON não clusterizado. Este tipo de índice é uma boa maneira de combinar dados JSON e de colunas em consultas e criar índices otimizados para sua carga de trabalho.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>Os índices JSON são índices com reconhecimento de ordenação  
Um recurso importante dos índices sobre dados JSON é que os índices têm reconhecimento de ordenação. O resultado da função `JSON_VALUE` usada ao criar uma coluna computada é um valor de texto que herda sua ordenação da expressão de entrada. Portanto, os valores no índice são ordenados usando as regras de ordenação definidas nas colunas de origem.  
  
Para demonstrar que os índices têm reconhecimento de ordenação, o exemplo a seguir cria uma tabela de ordenação simples com uma chave primária e conteúdo JSON.  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
O comando anterior especifica a ordenação Sérvio Cirílico para a coluna JSON. O exemplo a seguir preenche a tabela e cria um índice na propriedade de nome.  
  
```sql  
INSERT INTO JsonCollection
VALUES
(N'{"name":"Иво","surname":"Андрић"}'),
(N'{"name":"Андрија","surname":"Герић"}'),
(N'{"name":"Владе","surname":"Дивац"}'),
(N'{"name":"Новак","surname":"Ђоковић"}'),
(N'{"name":"Предраг","surname":"Стојаковић"}'),
(N'{"name":"Михајло","surname":"Пупин"}'),
(N'{"name":"Борислав","surname":"Станковић"}'),
(N'{"name":"Владимир","surname":"Грбић"}'),
(N'{"name":"Жарко","surname":"Паспаљ"}'),
(N'{"name":"Дејан","surname":"Бодирога"}'),
(N'{"name":"Ђорђе","surname":"Вајферт"}'),
(N'{"name":"Горан","surname":"Бреговић"}'),
(N'{"name":"Милутин","surname":"Миланковић"}'),
(N'{"name":"Никола","surname":"Тесла"}')
GO
  
ALTER TABLE JsonCollection
ADD vName AS JSON_VALUE(json,'$.name')

CREATE INDEX idx_name
ON JsonCollection(vName)
```  
  
Os comandos anteriores criam um índice padrão na coluna computada `vName`, que representa o valor da propriedade JSON `$.name`. Na página de código Sérvio Cirílico, a ordem das letras é 'А','Б','В','Г','Д','Ђ','Е', etc. A ordem dos itens no índice está em conformidade com as regras do Sérvio Cirílico, pois o resultado da função `JSON_VALUE` herda sua ordenação da coluna de origem. O exemplo a seguir consulta esse agrupamento e classifica os resultados por nome.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Se você examinar o plano de execução real, verá que ele usa valores classificados do índice não clusterizado.  
  
 ![Captura de tela mostrando um plano de execução que usa valores classificados do índice não clusterizado.](../../relational-databases/json/media/jsonindexblog2.png "Plano de execução")  
  
 Embora a consulta tenha uma cláusula `ORDER BY`, o plano de execução não usa um operador Sort. O índice JSON já é ordenado de acordo com a regras do Sérvio Cirílico. Portanto, o SQL Server pode usar o índice não clusterizado nos quais os resultados já estão classificados.  
  
 No entanto, se alterar a ordenação da expressão `ORDER BY` (por exemplo, se adicionar `COLLATE French_100_CI_AS_SC` após a função `JSON_VALUE`), você obterá um plano de execução de consulta diferente.  
  
 ![Captura de tela mostrando outro plano de execução.](../../relational-databases/json/media/jsonindexblog3.png "Plano de execução")  
  
 Como a ordem dos valores no índice não segue as regras de ordenação do Francês, o SQL Server não pode usar o índice para ordenar os resultados. Portanto, ele adiciona um operador Sor que classifica os resultados usando as regras de ordenação do Francês.  
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
