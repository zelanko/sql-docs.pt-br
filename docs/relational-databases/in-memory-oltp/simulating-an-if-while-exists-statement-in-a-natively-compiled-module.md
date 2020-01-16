---
title: Como similar IF-WHILE EXISTS – módulo compilado nativamente
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
ms.openlocfilehash: e860bbab32549b72048d30caa93f18daa422cc42
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412601"
---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>Simulando uma Instrução IF-WHILE EXISTS em um Módulo Compilado de Forma Nativa
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

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
  
  
