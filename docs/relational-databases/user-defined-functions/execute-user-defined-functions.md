---
title: "Executar fun&#231;&#245;es definidas pelo usu&#225;rio | Microsoft Docs"
ms.custom: ""
ms.date: "10/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-udf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "invocando funções definidas pelo usuário"
  - "user-defined functions [SQL Server], executing"
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
caps.latest.revision: 35
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 35
---
# Executar fun&#231;&#245;es definidas pelo usu&#225;rio
  Execute uma função definida pelo usuário usando o Transact-SQL.
  

> **Observação:** visite [função definida pelo usuário](https://msdn.microsoft.com/library/ms191007.aspx) e [Criar função (Transact SQL](https://msdn.microsoft.com/library/ms186755.aspx) para saber mais sobre funções definidas pelo usuário. 
  
 
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 No Transact-SQL, os parâmetros podem ser fornecidos usando *valor* ou usando @*parameter_name*=*valor.* . Um parâmetro não faz parte de uma transação; portanto, se um parâmetro for alterado em uma transação que for posteriormente revertida, o parâmetro não será revertido para seu valor anterior. O valor retornado ao chamador será sempre o valor no momento do retorno do módulo.  
  
###  <a name="Security"></a> Segurança  
  
 Não são solicitadas permissões para executar a instrução [EXECUTE](https://msdn.microsoft.com/library/ms188332.aspx). Porém, permissões **são necessárias** nos protegíveis mencionados na cadeia de caracteres EXECUTE. Por exemplo, se a cadeia de caracteres tiver uma instrução [INSERT](https://msdn.microsoft.com/library/ms174335.aspx), o chamador da instrução EXECUTE deverá ter a permissão INSERT na tabela de destino. As permissões são verificadas quando a instrução EXECUTE for encontrada, mesmo se ela estiver incluída em um módulo. Para obter mais informações, veja [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
### Exemplo 
  
Este exemplo usa a função de valor escalar `ufnGetSalesOrderStatusText` que está disponível na maioria das edições do `AdventureWorks`.  A finalidade da função é retornar um valor de texto para o status de vendas de um determinado inteiro.  Varie o exemplo passando números inteiros de 1 a 7 para o parâmetro **\@Status**.
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  