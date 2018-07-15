---
title: Categoria de trabalho de envio de logs de SQL Server Agent causa falha na atualização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
caps.latest.revision: 16
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a0e235b33ae24ff823e8492690e6775951dc4ef8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37242226"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>Categoria do trabalho Envio de Logs do SQL Server Agent causa falha na atualização
  O processo de atualização falhará se uma categoria de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, nomeada Envio de Log, existir.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Description  
 Há uma categoria de trabalho do sistema chamada Envio de Logs. Se uma instalação que está sendo atualizada tiver uma categoria de trabalho criada pelo usuário com esse nome, o nome deverá ser alterado antes da atualização. Caso contrário, o processo de atualização falhará.  
  
## <a name="see-also"></a>Consulte também  
 [Envio de logs não será executado após a atualização](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [Atualização mudará a conta de Proxy de usuário do SQL Server Agent para UpgradedProxyAccount temporária](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
