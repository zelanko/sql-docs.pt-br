---
title: ':: (Resolução de escopo) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b2e6e7d28fb4b04b61c1cd1cf5877d231f220e76
ms.sourcegitcommit: 5ef24b3229b4659ede891b0af2125ef22bd94b96
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55759939"
---
# <a name="-scope-resolution-transact-sql"></a>:: (Resolução de escopo) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O operador de resolução de escopo **::** fornece acesso a membros estáticos de um tipo de dados composto. Um tipo de dados composto é aquele que contém vários tipos de dados simples e métodos. Tipos de dados compostos incluem os tipos CLR internos e UDTs (tipos definidos pelo usuário) SQLCLR personalizados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como usar o operador de resolução de escopo para acessar o membro `GetRoot()` do tipo `hierarchyid`.  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
 