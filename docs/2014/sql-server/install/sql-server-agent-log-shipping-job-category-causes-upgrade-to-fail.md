---
title: SQL Server Agent categoria de trabalho de envio de logs faz com que a atualização falhe | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2f5947e8fc8d459388fe35d86c75666e25b5d907
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036129"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>Categoria do trabalho Envio de Logs do SQL Server Agent causa falha na atualização
  O processo de atualização falhará se uma categoria de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, nomeada Envio de Log, existir.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Descrição  
 Há uma categoria de trabalho do sistema chamada Envio de Logs. Se uma instalação que está sendo atualizada tiver uma categoria de trabalho criada pelo usuário com esse nome, o nome deverá ser alterado antes da atualização. Caso contrário, o processo de atualização falhará.  
  
## <a name="see-also"></a>Consulte Também  
 [O envio de logs não será executado após a atualização](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [A atualização alterará o SQL Server Agent conta proxy do usuário para o UpgradedProxyAccount temporário](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
