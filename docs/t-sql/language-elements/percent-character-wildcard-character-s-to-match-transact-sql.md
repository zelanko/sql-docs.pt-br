---
description: Caractere de porcentagem (Curinga - Caracteres de Correspondência) (Transact-SQL)
title: Pesquisa com curinga (%)
ms.custom: seo-lt-2019
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '%'
- '%_TSQL'
- wildcard
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], wildcards
- '% (wildcard - character(s) to match)'
- matching conditions [SQL Server]
- wildcard characters [SQL Server]
- characters [SQL Server], wildcard
ms.assetid: d4cbc1a9-37e1-4101-97fb-e6ac30c1223e
author: rothja
ms.author: jroth
ms.openlocfilehash: 5a0c232b2849f2fcfc7bf7d0a946714b15f753fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88307545"
---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>Caractere de porcentagem (Curinga - Caracteres de Correspondência) (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Corresponde a qualquer cadeia de zero ou mais caracteres. Esse caractere curinga pode ser usado como um prefixo ou como um sufixo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os nomes das pessoas na tabela `Person` do `AdventureWorks2012` que começam com `Dan`.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Dan%';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91; &#93; (curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91;^&#93; (Curinga – caracteres para não correspondência)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (Curinga – Corresponde a um caractere)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
