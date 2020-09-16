---
description: 'Etapa 3: Prova de conceito da conexão ao SQL usando Ruby'
title: 'Etapa 3: Prova de conceito da conexão com o SQL usando o Ruby | Microsoft Docs'
ms.custom: ''
ms.date: 06/22/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3553f57191dc462067fc48dc1cf2394437912240
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484769"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Etapa 3: Prova de conceito da conexão ao SQL usando Ruby

Este exemplo só deve ser considerado como uma prova de conceito.  O código de exemplo está simplificado para fins de clareza e não necessariamente representa as melhores práticas recomendadas pela Microsoft.  
  
## <a name="step-1--connect"></a>Etapa 1:  Conectar  
  
A função [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) é usada para se conectar ao Banco de Dados SQL.  
  
```ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Etapa 2:  Executar uma consulta  
  
Copie e cole o código a seguir em um arquivo vazio. Nomeie-o como test.rb. Em seguida, execute-o digitando o seguinte comando no seu prompt de comando:  
  
```ruby
    ruby test.rb  
```
  
No exemplo de código, A função [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds) é usada para recuperar um conjunto de resultados de uma consulta no Banco de Dados SQL. Essa função aceita uma consulta e retorna um conjunto de resultados. O conjunto de resultados é iterado usando [result.each do |row|](https://github.com/rails-sqlserver/tiny_tds).  
  
```ruby 
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
  
## <a name="step-3--insert-a-row"></a>Etapa 3:  Inserir uma linha  
  
Neste exemplo, você verá como executar uma instrução [INSERT](../../t-sql/statements/insert-transact-sql.md) com segurança, passar parâmetros que protegem seu aplicativo contra o valor [injeção de SQL](../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
Para usar o TinyTDS com o Azure, recomendamos a execução de várias `SET` instruções para alterar o modo como a sessão atual lida com informações específicas. Instruções `SET` recomendadas são fornecidas no código de exemplo. Por exemplo, `SET ANSI_NULL_DFLT_ON` permitirá novas colunas criadas para permitir valores nulos, mesmo que o status de nulidade da coluna não seja declarado explicitamente.  
  
Para alinhar com o formato [datetime](../../t-sql/data-types/datetime-transact-sql.md) do Microsoft SQL Server, use a função [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) para conversão no formato de datetime correspondente.  
  
```ruby
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
