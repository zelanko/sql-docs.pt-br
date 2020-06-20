---
title: O envio de logs não será executado após a atualização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server]
ms.assetid: 6727cb7d-ac01-4972-a730-dbb7cdc29705
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b2af60743cb2cbf9bf455397fe052c4e81f5a06d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036628"
---
# <a name="log-shipping-will-not-run-after-upgrading"></a>Envio de log não executará após a atualização
  O Supervisor de Atualização detectou que você está usando envio de logs. O envio de log do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] não é compatível como o envio de log do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e não pode ser atualizado diretamente. Depois da atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], reconfigure o envio de log usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou procedimentos armazenados.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Agent categoria de trabalho de envio de logs faz com que a atualização falhe](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [A atualização alterará o SQL Server Agent conta proxy do usuário para o UpgradedProxyAccount temporário](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
