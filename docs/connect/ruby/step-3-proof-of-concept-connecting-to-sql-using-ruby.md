---
title: 'Etapa 3: Prova de conceito da conexão com o SQL usando o Ruby | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9724fb48f6ae896d9026bfec63056070e2180a8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992493"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Etapa 3: Prova de conceito da conexão ao SQL usando Ruby

Este exemplo deve ser considerado apenas uma prova de conceito.  O código de exemplo é simplificado para fins de clareza e não necessariamente representa as práticas recomendadas recomendadas pela Microsoft.  
  
## <a name="step-1--connect"></a>Etapa 1: conectar-se  
  
A função [função tinytds:: Client](https://github.com/rails-sqlserver/tiny_tds) é usada para se conectar ao banco de dados SQL.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Etapa 2: Executar uma consulta  
  
Copie e cole o código a seguir em um arquivo vazio. Chame-o de Test. rb. Em seguida, execute-o inserindo o seguinte comando no prompt de comando:  
  
    ruby test.rb  
  
No exemplo de código, a função [função tinytds:: Result](https://github.com/rails-sqlserver/tiny_tds) é usada para recuperar um conjunto de resultados de uma consulta no banco de dados SQL. Essa função aceita uma consulta e retorna um conjunto de resultados. O conjunto de resultados é iterado usando o [resultado. cada | linha |](https://github.com/rails-sqlserver/tiny_tds).  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>Etapa 3: inserir uma linha  
  
Neste exemplo, você verá como executar uma instrução [Insert](../../t-sql/statements/insert-transact-sql.md) com segurança, passar parâmetros que protegem seu aplicativo do valor de [injeção de SQL](../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
Para usar o função tinytds com o Azure, é recomendável executar várias `SET` instruções para alterar a forma como a sessão atual lida com informações específicas. As `SET` instruções recomendadas são fornecidas no exemplo de código. Por exemplo, `SET ANSI_NULL_DFLT_ON` permitirá novas colunas criadas para permitir valores nulos, mesmo se o status de nulidade da coluna não for explicitamente declarado.  
  
Para alinhar com o formato de [data e hora](../../t-sql/data-types/datetime-transact-sql.md) Microsoft SQL Server, use a função [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) para converter para o formato DateTime correspondente.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```
