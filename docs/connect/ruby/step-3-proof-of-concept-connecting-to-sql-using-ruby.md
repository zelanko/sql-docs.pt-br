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
manager: craigg
ms.openlocfilehash: f384f179983012d5acf4726fb641245ca8a2cfb2
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51599966"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Etapa 3: Prova de conceito da conexão ao SQL usando Ruby

Este exemplo deve ser considerado uma prova de conceito apenas.  O código de exemplo é simplificado por motivos de clareza e não representa necessariamente as melhores práticas recomendadas pela Microsoft.  
  
## <a name="step-1--connect"></a>Etapa 1: conectar-se  
  
O [tinytds:: Client](https://github.com/rails-sqlserver/tiny_tds) função é usada para se conectar ao banco de dados SQL.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Etapa 2: Executar uma consulta  
  
Copie e cole o código a seguir em um arquivo vazio. Chamá-lo RB. Em seguida, executá-lo, digitando o seguinte comando do prompt de comando:  
  
    ruby test.rb  
  
No exemplo de código, o [tinytds:: Result](https://github.com/rails-sqlserver/tiny_tds) função é usada para recuperar um conjunto de resultados de uma consulta no banco de dados SQL. Essa função aceita uma consulta e retorna um conjunto de resultados. O conjunto de resultados é iterado usando a tecla TAB [Result | linha |](https://github.com/rails-sqlserver/tiny_tds).  
  
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
  
Neste exemplo, você verá como executar uma [inserir](../../t-sql/statements/insert-transact-sql.md) instrução com segurança, passar parâmetros que protegem seu aplicativo contra [injeção de SQL](../../relational-databases/tables/primary-and-foreign-key-constraints.md) valor.    
  
Para usar o TinyTDS com o Azure, é recomendável que você execute várias `SET` instruções para alterar como a sessão atual lida com informações específicas. Recomendado `SET` instruções são fornecidas no código de exemplo. Por exemplo, `SET ANSI_NULL_DFLT_ON` permitirá novas colunas criadas para permitir valores nulos, mesmo se o status de nulidade da coluna não é explicitamente declarado.  
  
Para se alinhar com o Microsoft SQL Server [datetime](../../t-sql/data-types/datetime-transact-sql.md) Formatar, use o [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) função a ser convertido para o formato de data e hora correspondente.  
  
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
