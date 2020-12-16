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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0438806d15caf806c4598f3d2b3882011d77d0f5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485198"
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
 [Problemas de migração para procedimentos armazenados compilados nativamente](./a-guide-to-query-processing-for-memory-optimized-tables.md)   
 [Construções do Transact-SQL sem suporte pelo OLTP na memória](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
