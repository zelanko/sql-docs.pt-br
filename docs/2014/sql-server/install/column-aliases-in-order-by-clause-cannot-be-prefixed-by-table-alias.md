---
title: Aliases de coluna na cláusula ORDER BY não podem ser prefixados pelo alias de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- aliases [SQL Server], columns
ms.assetid: fee7328f-6e8d-4005-930b-56fb6f17e0b2
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 18c65604efb2d1b0ff93d09b8d03f7ee6cb213cd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011723"
---
# <a name="column-aliases-in-order-by-clause-cannot-be-prefixed-by-table-alias"></a>Aliases de coluna na cláusula ORDER BY não podem ter como prefixo o alias da tabela
  No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, aliases de coluna na cláusula ORDER BY não podem ter como prefixo o alias da tabela.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Por exemplo, a consulta a seguir executa no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], mas retorna uma erro no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.l  
```  
  
 O [!INCLUDE[ssDEversion10](../../includes/ssdeversion10-md.md)] não corresponde `p.l` na cláusula `ORDER BY` a uma coluna válida na tabela.  
  
### <a name="exception"></a>Exceção  
 Se o alias de coluna prefixado que é especificado na cláusula ORDER BY for um nome de coluna válido na tabela especificada, a consulta executará sem erro; no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a semântica da instrução pode ser diferente. Por exemplo, o alias de coluna (`id`) especificado na instrução a seguir é um nome de coluna válido na tabela `sysobjects`. No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], quando a instrução é executada, a operação `CAST` é executada depois que o conjunto de resultados é classificado. Isso significa a coluna `name` é usada na operação de classificação. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], a operação `CAST` acontece antes da operação de classificação. Isso significa que a coluna `id` na tabela é usada na operação de classificação e retorna o conjunto de resultados em uma ordem inesperada.  
  
```  
SELECT CAST (o.name AS char(128)) AS id  
FROM sysobjects AS o  
ORDER BY o.id;  
```  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique as consultas que usam aliases de coluna prefixados por aliases de tabelas na cláusula ORDER BY de uma das seguintes formas:  
  
-   Não coloque prefixo no alias de coluna da cláusula ORDER BY, se possível.  
  
-   Substitua o alias de coluna pelo nome da coluna.  
  
 Por exemplo, ambas as consultas a seguir executam sem erro no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY l  
  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.LastName  
```  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
