---
title: O Microsoft SharePoint 2007 está instalado (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6f1da295-d9b7-4948-99d3-ebd3587337c6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 84672ddf6a9b2912f3d53eef8d40727369376ba5
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952088"
---
# <a name="microsoft-sharepoint-2007-is-installed-upgrade-advisor"></a>O Microsoft SharePoint 2007 está instalado (Supervisor de Atualização)
  O Supervisor de Atualização detectou uma versão sem suporte de um produto ou uma tecnologia do SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não será atualizado ou instalado no SharePoint 2007. A atualização está bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para continuar com a atualização, você deve desinstalar o SharePoint 2007 ou atualizar o SharePoint 2007 para um produto do SharePoint 2010. Depois de atualizar sua instalação do SharePoint, execute novamente o Supervisor de Atualização para confirmar se não há outros problemas de atualização.  
  
 Não é possível atualizar diretamente do SharePoint 2007 para o SharePoint 2013. Mas você pode fazer o que é conhecido como um anexo de banco de dados "salto duplo" para atualizar do Office SharePoint Server 2007 para o SharePoint Server 2010 e, em seguida, do SharePoint Server 2010 para o SharePoint Server 2013.  
  
## <a name="see-also"></a>Consulte também  
 [Supervisor de atualização &#40;de problemas de atualização do Reporting Services&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
