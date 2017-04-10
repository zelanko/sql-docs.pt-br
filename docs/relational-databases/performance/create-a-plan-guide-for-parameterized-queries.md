---
title: "Criar um guia de plano para consultas parametrizadas | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-plan-guides"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "consultas parametrizadas, guias de plano para"
  - "guias de plano [SQL Server], consultas parametrizadas"
ms.assetid: b532ae16-66e7-4641-9bc8-b0d805853477
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Criar um guia de plano para consultas parametrizadas
  O guia de plano TEMPLATE corresponde consultas autônomas com parâmetros com uma forma especificada.  
  
 O exemplo a seguir cria um guia de plano que faz a correspondência de qualquer consulta com parâmetros com um formulário especificado, e direciona o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para forçar a aplicação de parâmetros da consulta. As duas consultas a seguir são sintaticamente equivalentes, mas só diferem nos valores literais constantes.  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 Este é o guia de plano na forma com parâmetros da consulta:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 No exemplo anterior, o valor do parâmetro `@stmt` é a forma com parâmetros da consulta. O único modo confiável de obter esse valor para uso em sp_create_plan_guide é por meio do procedimento armazenado do sistema [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md). O script a seguir pode ser usado para obter a consulta parametrizada e, em seguida, criar um guia de plano para ela.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  O valor dos literais constantes no parâmetro `@stmt` passado para `sp_get_query_template` pode afetar o tipo de dados escolhido para o parâmetro que substitui a literal. Isso afetará a correspondência do guia de plano. Pode ser necessário criar mais de um guia de plano para lidar com diferentes intervalos de valores de parâmetros.  
  
 Também é possível usar os guias de plano TEMPLATE com os guias de plano SQL. Por exemplo, você pode criar um guia de plano TEMPLATE para ter certeza que uma classe de consultas contém parâmetros. Em seguida, é possível criar um guia de plano SQL na forma com parâmetros dessa consulta.  
  
  