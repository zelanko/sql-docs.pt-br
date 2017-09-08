---
title: "Definir o escopo de operador de resolução (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f03f0c8274d52f61e5db2d75fe21e3fe90a4ce26
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="scope-resolution-operator-transact-sql"></a>Operador de resolução de escopo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O operador de resolução do escopo **::** fornece acesso a membros estáticos de um tipo de dados composto. Um tipo de dados composto é aquele que contém vários tipos de dados simples e métodos.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como usar o operador de resolução de escopo para acessar o membro `GetRoot()` do tipo `hierarchyid`.  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>Consulte também  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
