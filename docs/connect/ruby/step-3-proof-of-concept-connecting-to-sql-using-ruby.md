---
title: 'Etapa 3: Prova de conceito da conexão ao SQL usando o Ruby | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: ruby
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5bf98585281b4b84869c385c848d9add459d57b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Etapa 3: Prova de conceito da conexão ao SQL usando o Ruby

Este exemplo deve ser considerado uma prova de conceito apenas.  O código de exemplo é simplificado para maior clareza e não representa necessariamente práticas recomendadas pela Microsoft.  
  
## <a name="step-1--connect"></a>Etapa 1: conectar-se  
  
O [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) função é usada para se conectar ao banco de dados SQL.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Etapa 2: Executar uma consulta  
  
Copie e cole o código a seguir em um arquivo vazio. Ele chame test.rb. Em seguida, executá-lo, digitando o seguinte comando do prompt de comando:  
  
    ruby test.rb  
  
No exemplo de código, o [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds) função é usada para recuperar um conjunto de resultados de uma consulta no banco de dados SQL. Essa função aceita uma consulta e retorna um conjunto de resultados. O conjunto de resultados é iterado usando a tecla [result.each fazer | linha |](https://github.com/rails-sqlserver/tiny_tds).  
  
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
  
## <a name="step-3--insert-a-row"></a>Etapa 3: Inserir uma linha  
  
Neste exemplo, você verá como executar um [inserir](../../t-sql/statements/insert-transact-sql.md) instrução passar com segurança, os parâmetros que proteger seu aplicativo de [injeção SQL](../../relational-databases/tables/primary-and-foreign-key-constraints.md) valor.    
  
Para usar TinyTDS com o Azure, é recomendável que você execute várias `SET` instruções para alterar como a sessão atual controla informações específicas. Recomendado `SET` instruções são fornecidas no exemplo de código. Por exemplo, `SET ANSI_NULL_DFLT_ON` permitirá novas colunas criadas para permitir valores nulos, mesmo se o status de nulidade da coluna não é explicitamente declarado.  
  
Para alinhar com o Microsoft SQL Server [datetime](http://msdn.microsoft.com/library/ms187819.aspx) de formato, use o [strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) função converter no formato de data e hora correspondente.  
  
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
