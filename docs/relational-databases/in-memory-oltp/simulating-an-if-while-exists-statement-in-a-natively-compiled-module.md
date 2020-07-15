---
title: Como similar IF-WHILE EXISTS – módulo compilado nativamente
description: Saiba como simular a cláusula EXISTS em instruções condicionais, que não são compatíveis com procedimentos armazenados compilados nativamente no SQL Server.
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f62b799a124eb7ed47ffad9e63d0433172984c18
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735016"
---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>Simulando uma Instrução IF-WHILE EXISTS em um Módulo Compilado de Forma Nativa
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Os procedimentos armazenados compilados de forma nativa não dão suporte à cláusula **EXISTS** em instruções condicionais como IF e WHILE.  
  
 O exemplo a seguir ilustra uma solução alternativa usando uma variável BIT com uma instrução SELECT para simular uma cláusula EXISTS:  
  
```sql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE ...  
IF @exists = 1  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de migração para procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construções do Transact-SQL sem suporte pelo OLTP na memória](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
