---
title: Aplicar um plano de consulta fixo a um guia de plano | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: bbf401f9-af7c-48e7-8a43-bf25e8af2fd7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0afa2d8770589ed82890cf5b54e99916f9eb1d00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150955"
---
# <a name="apply-a-fixed-query-plan-to-a-plan-guide"></a>Aplicar um plano de consulta fixo a um guia de plano
  É possível aplicar um plano de consulta fixo a um guia de plano do tipo OBJECT ou SQL. Os guias de plano que se aplicam a um plano de consulta fixo são úteis quando se conhece um plano de execução existente que é melhor do que aquele selecionado pelo otimizador para uma consulta específica.  
  
 O exemplo a seguir cria um guia de plano para uma instrução SQL ad hoc simples. Especifique o XML Showplan para a consulta diretamente no parâmetro `@hints` para que o plano de consulta desejado para essa instrução seja fornecido no guia de plano. O exemplo executa a instrução SQL primeiro para gerar um plano no cache do esquema. Nesse exemplo, supõe-se que o plano gerado é o desejado e que nenhum ajuste de consulta adicional é necessário. O Plano de execução XML da consulta é obtido por meio da consulta das exibições de gerenciamento dinâmico `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`e `sys.dm_exec_text_query_plan` e é atribuído à variável `@xml_showplan` . Em seguida, a variável `@xml_showplan` é passada à instrução `sp_create_plan_guide` no parâmetro `@hints` . Também é possível criar um guia de plano com base em um plano de consulta no cache de plano por meio do procedimento armazenado [sp_create_plan_guide_from_handle](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql) .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = @xml_showplan;  
GO  
```  
  
  
