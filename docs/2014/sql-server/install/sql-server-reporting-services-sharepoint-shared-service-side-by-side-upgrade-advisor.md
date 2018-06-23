---
title: Microsoft SQL Server Reporting Services serviço compartilhado do SharePoint é instalada lado a lado (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 79f07ede92ee840ed50631c10d22bf4b015cf29b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010612"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>O serviço compartilhado do SharePoint do Microsoft SQL Server Reporting Services está instalado lado a lado (Supervisor de Atualização)
  Supervisor de atualização detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço compartilhado do SharePoint é instalado lado a lado com uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 Supervisor de atualização detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço compartilhado do SharePoint é instalado lado a lado com uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que não se baseia na arquitetura de serviço compartilhado do SharePoint. Como o computador tem as tecnologias mais antigas e mais recentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint instaladas lado a lado, a atualização está bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para continuar com a atualização, você deve desinstalar uma das instalações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] existentes. Depois de remover uma das instalações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], execute novamente o Supervisor de Atualização para confirmar se não há outros problemas de atualização.  
  
  