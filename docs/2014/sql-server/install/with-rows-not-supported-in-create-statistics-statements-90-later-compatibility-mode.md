---
title: Não há suporte para com linhas na instrução CREATE STATISTICS no modo de compatibilidade 90 ou posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7318340d5bf5e5861c1a95d6fa8cc9e54679f4a5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137506"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>Não há suporte para WITH ROWS na instrução CREATE STATISTICS no modo de compatibilidade 90 ou posterior
  Não há suporte para WITH ROWS na instrução CREATE STATISTICS quando você executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurado no modo de compatibilidade 90 ou posterior.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique as instruções CREATE STATISTICS que contenham WITH ROWS especificando WITH SAMPLE *número* linhas, ou especificando outras opções que estão em conformidade com a sintaxe do documento. Para obter mais informações, consulte o tópico ‘CREATE STATISTICS (Transact-SQL)’ nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
