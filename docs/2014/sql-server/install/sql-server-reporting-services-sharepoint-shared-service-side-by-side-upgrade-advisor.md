---
title: Microsoft SQL Server Reporting Services serviço compartilhado do SharePoint está instalado lado a lado (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b8a26fedd892dfb26dea4616efd46d3b3748b508
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85035990"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>O serviço compartilhado do SharePoint do Microsoft SQL Server Reporting Services está instalado lado a lado (Supervisor de Atualização)
  O supervisor de atualização detectou que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o serviço compartilhado do SharePoint está instalado lado a lado com uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O supervisor de atualização detectou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que o serviço compartilhado do SharePoint está instalado lado a lado com uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que não é baseada na arquitetura do serviço compartilhado do SharePoint. Como o computador tem as tecnologias mais antigas e mais recentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint instaladas lado a lado, a atualização está bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para continuar com a atualização, você deve desinstalar uma das instalações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] existentes. Depois de remover uma das instalações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], execute novamente o Supervisor de Atualização para confirmar se não há outros problemas de atualização.  
  
  
