---
title: WITH ROWS não tem suporte em instruções CREATE STATISTICs no modo de compatibilidade de 90 ou posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e48602f61c09a8de76e2894a4fa808b2f39f4cbe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66090967"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>Não há suporte para WITH ROWS na instrução CREATE STATISTICS no modo de compatibilidade 90 ou posterior
  Não há suporte para WITH ROWS na instrução CREATE STATISTICS quando você executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurado no modo de compatibilidade 90 ou posterior.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique as instruções CREATE STATISTICs que incluem com linhas especificando com linhas de *número* de exemplo ou especificando outras opções que estão em conformidade com a sintaxe documentada. Para obter mais informações, consulte o tópico ‘CREATE STATISTICS (Transact-SQL)’ nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
