---
title: Operadores de junção externa *= e =* não têm suporte no modo de compatibilidade 90 ou posterior | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- =* join
- '*= join'
- joins [SQL Server]
ms.assetid: ca4aa11f-1048-411f-9c6c-3d0a8e319f2f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6d5d9ff66bb078be30fcd6e7d4b43b5e94069be0
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591610"
---
# <a name="outer-join-operators--and--are-not-supported-in-90-or-later-compatibility-modes"></a>Os operadores de junção externa \*= e =\* não são compatíveis com o modo de compatibilidade 90 ou posterior
  O Supervisor de atualização detectou o uso de operadores de junção externa \*= e =\*. Esses operadores não são aceitos no modo de compatibilidade 90 ou posterior. Quando você faz a atualização, os bancos de dados de usuários mantêm seus modos de compatibilidade. As instruções que usam esses operadores falhará.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes de alterar o modo de compatibilidade do banco de dados para 90 ou posterior, modifique as instruções que usam os operadores de junção externa \*= e =\* usar palavras-chave de junção externa equivalentes. O exemplo a seguir mostra uma consulta que usa o operador `\*=` e uma consulta equivalente que usa as palavras-chave `LEFT OUTER JOIN`.  
  
```  
-- This query uses an old-style outer join operator.  
USE pubs  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee, jobs   
WHERE employee.job_id *= jobs.job_id  
ORDER BY employee.job_id  
  
-- This query uses the ANSI standard keywords LEFT OUTER JOIN.  
USE pubs;  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
ORDER BY employee.job_id  
```  
  
 Para obter mais informações sobre junções externas, consulte "Usando junções externas" nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
