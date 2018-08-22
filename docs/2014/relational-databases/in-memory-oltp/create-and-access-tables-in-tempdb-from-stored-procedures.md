---
title: Criando e acessando tabelas em TempDB de procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b187186b573a70a3f3a03a408099bcb307798370
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394805"
---
# <a name="creating-and-accessing-tables-in-tempdb-from-natively-compiled-stored-procedures"></a>Criando e acessando tabelas em TempDB de procedimentos armazenados nativamente compilados
  Não há suporte para criar e acessar tabelas em TempDB de procedimentos armazenados nativamente compilados. Use tipos e variáveis de tabela. Por exemplo:  
  
```tsql  
CREATE TYPE dbo.OrderQuantityByProduct   
  AS TABLE   
   (id INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=100000),   
    ProductID INT NOT NULL,   
    Quantity INT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
GO  
CREATE PROCEDURE dbo.usp_OrderQuantityByProduct   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = 'english'  
)  
  -- declare table variables for the list of orders   
  DECLARE @Input dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @Input SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de migração para procedimentos armazenados compilados nativamente](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construções do Transact-SQL sem suporte pelo OLTP na memória](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
