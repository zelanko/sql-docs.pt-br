---
title: Especifique a palavra-chave WITH ao usar dicas de tabela no modo de compatibilidade 90 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ffa920d49bac601354d9364dd308c94696def46
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227196"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>Especificar a palavra-chave WITH ao usar dicas de tabela no modo de compatibilidade 90
  Com algumas exceções, há suporte para dicas de tabela na cláusula FROM de uma consulta somente quando as dicas são especificadas usando a palavra-chave WITH. Para obter mais informações, consulte os tópicos ‘FROM ([!INCLUDE[tsql](../../includes/tsql-md.md)])’ e ‘Dicas de tabela ([!INCLUDE[tsql](../../includes/tsql-md.md)]) ’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique as consultas que incluem dicas de tabela na cláusula FROM incluindo a palavra-chave WITH antes das dicas de tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
