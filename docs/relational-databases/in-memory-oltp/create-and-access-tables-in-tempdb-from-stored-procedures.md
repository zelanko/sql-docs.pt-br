---
title: Criar e acessar tabelas no TempDB de procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0db885db7e3138b4a863dc93a022950a8a30a5ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915323"
---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>Criar e acessar tabelas no TempDB de procedimentos armazenados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Não há suporte para criar e acessar tabelas em TempDB de procedimentos armazenados nativamente compilados. Em vez disso, use as tabelas com otimização de memória com DURABILITY=SCHEMA_ONLY ou use tipos de tabela e variáveis de tabela. 

Para saber detalhes sobre a otimização de memória da tabela temporária e os cenários de variável de tabela, confira: [Tabela temporária e variável de tabela mais rápidas usando a otimização de memória](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).
  
  O exemplo a seguir mostra como o uso de uma tabela temporária com três colunas (id, ProductID, Quantity) pode ser substituído usando uma variável de tabela **@OrderQuantityByProduct** do tipo **dbo.OrderQuantityByProduct**:  
  
```sql  
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
    LANGUAGE = N'ENGLISH'  
)  
  -- declare table variables for the list of orders   
  DECLARE @OrderQuantityByProduct dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @OrderQuantityByProduct SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de migração para procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construções do Transact-SQL sem suporte pelo OLTP na memória](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
