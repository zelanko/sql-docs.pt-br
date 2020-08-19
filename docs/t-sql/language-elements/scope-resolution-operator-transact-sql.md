---
description: ':: (Resolução de escopo) (Transact-SQL)'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1372950c3262f86ca1b0d85ca7026d6560f4afb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459269"
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
 
