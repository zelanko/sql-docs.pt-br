---
title: "Dados JSON do índice | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 3ed7a51b28d2b17b3239f971d0f4f684bec145cd
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
# <a name="index-json-data"></a>Indexar dados JSON
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

No SQL Server 2016, JSON não é um tipo de dados internas e do SQL Server não tem índices JSON personalizados. Você pode otimizar suas consultas em documentos JSON, no entanto, usando índices padrão. 

Índices de banco de dados melhoram o desempenho das operações de filtro e classificação. Sem índices, o SQL Server precisa executar uma verificação de tabela completa sempre que você consultar dados.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indexar propriedades com colunas computadas  
Ao armazenar dados JSON no SQL Server, normalmente você deseja filtrar ou classificar resultados de consulta por um ou mais *propriedades* dos documentos JSON.  

### <a name="example"></a>Exemplo 
Neste exemplo, suponha que o AdventureWorks `SalesOrderHeader` tabela tem um `Info` coluna que contém várias informações em formato JSON sobre ordens de venda. Por exemplo, ele contém informações sobre o cliente, vendedor, endereços de envio e de cobrança e assim por diante. Para usar valores da `Info` coluna para filtrar as ordens de venda para um cliente.

### <a name="query-to-optimize"></a>Consulta a otimizar
Aqui está um exemplo do tipo de consulta que você deseja otimizar o uso de um índice.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>Índice de exemplo
Se você quiser acelerar seus filtros ou `ORDER BY` cláusulas em uma propriedade de um documento JSON, você pode usar os mesmos índices que você já estiver usando em outras colunas. No entanto, não é possível *diretamente* fazer referência a propriedades em documentos JSON.
    
1.  Primeiro, você precisa criar uma "coluna virtual" que retorna os valores que você deseja usar para filtragem.
2.  Em seguida, crie um índice na coluna virtual.  
  
O exemplo a seguir cria uma coluna computada que pode ser usada para indexação. Em seguida, ele cria um índice na nova coluna computada. Este exemplo cria uma coluna que expõe o nome do cliente, que é armazenado no `$.Customer.Name` caminho nos dados JSON. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>Para obter mais informações sobre a coluna computada 
A coluna computada não é persistente. Ela é computada apenas quando o índice precisa ser recriado. Ela não ocupa espaço adicional na tabela.   
  
É importante que você criar a coluna computada com a mesma expressão que você planeja usar em suas consultas - neste exemplo, a expressão é `JSON_VALUE(Info, '$.Customer.Name')`.  
  
Não é preciso reescrever as consultas. Se você usar expressões com o `JSON_VALUE` função, conforme mostrado na consulta de exemplo acima, o SQL Server vê que existe uma coluna computada equivalente com a mesma expressão e aplica um índice, se possível.

### <a name="execution-plan-for-this-example"></a>Plano de execução para este exemplo
Aqui está o plano de execução para a consulta neste exemplo.  
  
![Plano de execução](../../relational-databases/json/media/jsonindexblog1.png "Plano de execução")  
  
Em vez de uma verificação completa, o SQL Server usa uma busca de índice no índice não clusterizado e localiza as linhas que atendem às condições especificadas. Em seguida, ele usa uma pesquisa de chave no `SalesOrderHeader` tabela para buscar outras colunas referenciadas na consulta - neste exemplo, `SalesOrderNumber` e `OrderDate`.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>Otimizar o índice com colunas incluídas
Se você adicionar as colunas necessárias no índice, você pode evitar essa pesquisa adicional na tabela. Você pode adicionar essas colunas como colunas incluídas padrão, conforme mostrado no exemplo a seguir, que estende o `CREATE INDEX` exemplo mostrado acima.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
Nesse caso o SQL Server não tem que ler dados adicionais a `SalesOrderHeader` como tudo o que precisa está incluído no índice JSON não clusterizado de tabela. Isso é uma boa maneira de combinar dados JSON e de colunas em consultas e criar índices otimizados para sua carga de trabalho.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>Os índices JSON são índices com reconhecimento de agrupamento  
Um recurso importante do índices sobre dados JSON é que os índices têm reconhecimento de agrupamento. O resultado da `JSON_VALUE` função que você usa ao criar a coluna computada é um valor de texto que herda seu agrupamento da expressão de entrada. Portanto, os valores no índice são ordenados usando as regras de agrupamento definidas nas colunas de origem.  
  
Para demonstrar isso, o exemplo a seguir cria uma tabela de agrupamento simples com uma chave primária e conteúdo JSON.  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
O comando anterior especifica o agrupamento Sérvio Cirílico para a coluna JSON. O exemplo a seguir preenche a tabela e cria um índice na propriedade de nome.  
  
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
  
Os comandos anteriores criam um índice padrão na coluna computada `vName`, que representa o valor do JSON `$.name` propriedade. Na página de código Sérvio Cirílico, a ordem das letras é "А", "Б", "В", "Г", "Д", "Ђ", "Е" etc. A ordem dos itens no índice está em conformidade com as regras do Sérvio cirílico porque o resultado da `JSON_VALUE` função herda seu agrupamento da coluna de origem. O exemplo a seguir consulta esse agrupamento e classifica os resultados por nome.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Se você examinar o plano de execução real, verá que ele usa valores classificados do índice não clusterizado.  
  
 ![Plano de execução](../../relational-databases/json/media/jsonindexblog2.png "Plano de execução")  
  
 Embora a consulta tenha uma `ORDER BY` cláusula, o plano de execução não usa um operador Sort. O índice JSON já é ordenado de acordo com a regras do Sérvio Cirílico. Portanto, o SQL Server pode usar o índice não clusterizado nos quais os resultados já estão classificados.  
  
 No entanto, se alterarmos o agrupamento do `ORDER BY` expressão - por exemplo, se colocarmos `COLLATE French_100_CI_AS_SC` depois que o `JSON_VALUE` função - obtemos um plano de execução de consulta diferentes.  
  
 ![Plano de execução](../../relational-databases/json/media/jsonindexblog3.png "Plano de execução")  
  
 Como a ordem dos valores no índice não segue as regras de agrupamento do Francês, o SQL Server não pode usar o índice para ordenar os resultados. Portanto, ele adiciona um operador Sor que classifica os resultados usando as regras de agrupamento do Francês.  
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Saiba mais sobre o suporte interno a JSON no SQL Server  
Para muitas soluções específicas, casos de uso e recomendações, consulte o [postagens no blog sobre o suporte interno a JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) no SQL Server e no banco de dados SQL Azure por Jovan Popovic, gerente de programas da Microsoft.

