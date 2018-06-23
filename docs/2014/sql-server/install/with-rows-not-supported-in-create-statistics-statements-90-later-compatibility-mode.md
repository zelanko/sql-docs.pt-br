---
title: Não há suporte para com linhas na instrução CREATE STATISTICS no modo de compatibilidade 90 ou posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9d509352d99cab9359e7ea222f5fb2d5d7e28075
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115340"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>Não há suporte para WITH ROWS na instrução CREATE STATISTICS no modo de compatibilidade 90 ou posterior
  Não há suporte para WITH ROWS na instrução CREATE STATISTICS quando você executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurado no modo de compatibilidade 90 ou posterior.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique as instruções CREATE STATISTICS que inclui WITH ROWS especificando WITH SAMPLE *número* linhas, ou especificando outras opções que estão em conformidade com a sintaxe do documento. Para obter mais informações, consulte o tópico ‘CREATE STATISTICS (Transact-SQL)’ nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
