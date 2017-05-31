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
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf3c58c7d71a98bfaa1f27611762bf7fb3fe8725
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="index-json-data"></a>Indexar dados JSON
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Índices de bancos de dados melhoram o desempenho de suas operações de filtragem e classificação. Sem índices, o SQL Server precisa executar uma verificação de tabela completa sempre que você consultar dados.  
  
 JSON não é um tipo de dados interno do SQL Server 2016, e o SQL Server 2016 não tem índices JSON personalizados. No entanto, você pode otimizar suas consultas em documentos JSON usando índices padrão.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indexar propriedades com colunas computadas  
 Ao armazenar dados JSON no SQL Server, normalmente você deseja filtrar ou classificar resultados de consulta pelas propriedades dos documentos JSON.  
  
 Neste exemplo, a tabela AdventureWorks SalesOrderHeader tem uma coluna "Info" que contém várias informações sobre pedidos de venda - por exemplo, informações sobre o cliente, o vendedor, endereços de envio/cobrança e assim por diante. Você deseja usar os valores da coluna Info para filtrar os pedidos de venda para um cliente. Veja a consulta que você deseja otimizar com o uso de um índice.  
  
```tsql  
SELECT SalesOrderNumber,OrderDate,JSON_VALUE(Info,'$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info,'$.Customer.Name')=N'Aaron Campbell' 
```  
  
 Se quiser acelerar seus filtros ou cláusulas ORDER BY em uma propriedade de um documento JSON, você pode usar os mesmos índices usados em outras colunas. No entanto, não é possível fazer referências diretas a propriedades em documentos JSON. Primeiro, você deve criar uma "coluna virtual" que retorna os valores que você deseja usar para filtragem. Em seguida, crie um índice na coluna virtual.  
  
 O exemplo a seguir cria uma coluna computada que pode ser usada para indexação e cria um índice nessa coluna. Esse exemplo cria uma coluna que expõe o nome do cliente, que é armazenado no caminho$.Customer.Name em documentos JSON.  
  
```tsql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
  
 A coluna computada não é persistente. Ela não ocupa espaço adicional na tabela. Ela é computada apenas quando o índice precisa ser recriado.  
  
 É importante criar a coluna computada com a mesma expressão que você planeja usar em suas consultas – neste exemplo, `JSON_VALUE(Info, '$.Customer.Name')`.  
  
 Não é preciso reescrever as consultas. Se você usar expressões com a função JSON_VALUE, o SQL Server vê que existe uma coluna computada equivalente com a mesma expressão e aplica um índice, se possível. Veja o plano de execução para a consulta no exemplo.  
  
 ![Plano de execução](../../relational-databases/json/media/jsonindexblog1.png "Plano de execução")  
  
 Em vez de uma verificação completa, o SQL Server usa uma busca de índice no índice não clusterizado e localiza as linhas que atendem às condições especificadas. Em seguida, ele usa uma pesquisa de chave na tabela SalesOrderHeader para buscar outras colunas referenciadas na consulta - neste exemplo, SalesOrderNumber e OrderDate.  
  
 Ao adicionar as colunas necessárias no índice JSON, você pode evitar essa pesquisa adicional na tabela. É possível adicionar essas colunas como colunas incluídas padrão, conforme é mostrado no exemplo a seguir.  
  
```tsql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
 Nesse caso o SQL Server não lê dados adicionais da tabela SalesOrderHeader, pois tudo de que ele precisa está incluído no índice JSON não clusterizado. Essa é uma boa maneira de combinar dados JSON e de colunas em consultas e criar índices otimizados para sua carga de trabalho.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>Os índices JSON são índices com reconhecimento de agrupamento  
 Um recurso importante do índices JSON é que eles têm reconhecimento de agrupamento. O resultado da função JSON_VALUE é um valor de texto que herda seu agrupamento da expressão de entrada. Portanto, os valores no índice são ordenados usando as regras de agrupamento definidas nas colunas de origem.  
  
 Para demonstrar isso, o exemplo a seguir cria uma tabela de agrupamento simples com uma chave primária e conteúdo JSON.  
  
```tsql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
 O comando anterior especifica o agrupamento Sérvio Cirílico para a coluna JSON. O exemplo a seguir preenche a tabela e cria um índice na propriedade de nome.  
  
```tsql  
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
  
 Os comandos anteriores criam um índice padrão na coluna computada vName, que representa o valor da propriedade JSON $.name. Na página de código Sérvio Cirílico, a ordem das letras é "А", "Б", "В", "Г", "Д", "Ђ", "Е" etc. A ordem dos itens no índice segue as regras do Sérvio Cirílico, pois o resultado da função JSON_VALUE herda seu agrupamento da coluna de origem. O exemplo a seguir consulta esse agrupamento e classifica os resultados por nome.  
  
```tsql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Se você examinar o plano de execução real, verá que ele usa valores classificados do índice não clusterizado.  
  
 ![Plano de execução](../../relational-databases/json/media/jsonindexblog2.png "Plano de execução")  
  
 Embora a consulta tenha uma cláusula ORDER BY, o plano de execução não usa um operador Sort. O índice JSON já é ordenado de acordo com a regras do Sérvio Cirílico. Portanto, o SQL Server pode usar o índice não clusterizado nos quais os resultados já estão classificados.  
  
 No entanto, se alterarmos o agrupamento da expressão ORDER BY (por exemplo, se colocarmos `COLLATE French_100_CI_AS_SC` após a função JSON_VALUE), obtemos um plano de execução de consulta diferente.  
  
 ![Plano de execução](../../relational-databases/json/media/jsonindexblog3.png "Plano de execução")  
  
 Como a ordem dos valores no índice não segue as regras de agrupamento do Francês, o SQL Server não pode usar o índice para ordenar os resultados. Portanto, ele adiciona um operador Sor que classifica os resultados usando as regras de agrupamento do Francês.  
  
  

