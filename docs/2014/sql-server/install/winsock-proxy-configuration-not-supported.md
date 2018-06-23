---
title: Configuração do Winsock Proxy não tem suportada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Winsock proxy configuration [SQL Server]
ms.assetid: abf71f7b-8bd7-49d2-92f7-9ddf72924d8c
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9b8af65a848d21fd04de9fe28d11160f3007a6d7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116060"
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
  
  
