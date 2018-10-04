---
title: PARA procurar não é permitida em exibições nos modos de compatibilidade 90 ou posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ccd82fd7b971c97319daa480ba3f9a222d026280
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065506"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>FOR BROWSE não é permitido em exibições nos modos de compatibilidade 90 ou posterior
  O Supervisor de Atualização detectou o uso da cláusula FOR BROWSE em uma exibição. A cláusula FOR BROWSE é permitida (e ignorada) em exibições quando o modo de compatibilidade do banco de dados está definido como 80. Entretanto, essa cláusula não é permitida em exibições quando o modo de compatibilidade do banco de dados está definido como 90 ou posterior.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Quando você faz a atualização, os bancos de dados de usuários mantêm seus modos de compatibilidade. Antes de alterar o modo de compatibilidade do banco de dados para 90 ou posterior, remova a cláusula FOR BROWSE das definições de exibição. Para obter mais informações, consulte ‘sp_dbcmptlevel’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
