---
title: Configuração do Winsock Proxy não tem suportada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Winsock proxy configuration [SQL Server]
ms.assetid: abf71f7b-8bd7-49d2-92f7-9ddf72924d8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7552218608ff06c7b9f0bd828c97faf1f7e0998a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108106"
---
# <a name="winsock-proxy-configuration-not-supported"></a>Não há suporte para a configuração do proxy Winsock
  O proxy Winsock não pode ser configurado usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ferramentas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 As ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem configurar componentes do Windows.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Use o Microsoft ISA (Internet Security and Acceleration) Server para publicar um computador. Para obter informações sobre como configurar o proxy Winsock, consulte a sua documentação do servidor de proxy.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
