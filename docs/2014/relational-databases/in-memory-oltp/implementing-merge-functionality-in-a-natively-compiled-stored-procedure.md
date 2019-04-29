---
title: Implementando a funcionalidade MERGE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0e108f70f66aef1ed88ea202ddb326bd0757c10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63015917"
---
# <a name="implementing-merge-functionality"></a>Implementando a funcionalidade MERGE
  Um banco de dados pode precisar executar uma inserção ou uma atualização, dependendo de uma linha específica já existir no banco de dados.  
  
 Sem usar a instrução `MERGE`, veja a seguir uma abordagem que pode ser usada no [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```sql  
UPDATE mytable SET col=@somevalue WHERE myPK = @parm  
IF @@ROWCOUNT = 0  
    INSERT mytable (columns) VALUES (@parm, @other values)  
```  
  
 Outro método do [!INCLUDE[tsql](../../includes/tsql-md.md)] para implementar uma mesclagem:  
  
```sql  
IF EXISTS (SELECT 1 FROM mytable WHERE myPK = @parm)  
    UPDATE....  
ELSE  
    INSERT  
```  
  
 Para um procedimento armazenado nativamente compilado  
  
```sql  
DECLARE @i  int  = 0  -- or whatever your PK data type is  
UPDATE mytable SET @i=myPK, othercolums = other values WHERE myPK = @parm  
IF @i = 0  
   INSERT....  
```  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de migração para procedimentos armazenados compilados nativamente](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construções do Transact-SQL sem suporte pelo OLTP na memória](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
