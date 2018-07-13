---
title: Aplicar um plano de consulta fixo a um guia de plano | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bbf401f9-af7c-48e7-8a43-bf25e8af2fd7
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ac69187ec760c8ca9af0e7346a2f8b4c88fd5af3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419445"
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
  
  
