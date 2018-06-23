---
title: Banco de dados de servidor de relatório não está configurado (Supervisor de atualização) | Microsoft Docs
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
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f86e9963750d2bacbdc55e235e4975a05c2f625e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020843"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>O banco de dados do servidor de relatório não está configurado (Supervisor de Atualização)
  A atualização está bloqueada devido a uma configuração incompleta do servidor de relatório. O banco de dados do servidor de relatório não está configurado.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 A Instalação só pode atualizar uma instância do servidor de relatório completamente configurada. Para continuar, você deve configurar o banco de dados do servidor de relatório, ou use o Microsoft Windows **painel de controle** para remover o recurso do servidor de relatório a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação. Depois de remover o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é possível atualizar outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Caso não tenha configurado o banco de dados do servidor de relatório, o servidor de relatório não estará operacional e deverá ser removido antes da atualização.  
  
 Para obter informações adicionais sobre a desinstalação [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte [desinstalar o Reporting Services 2012](http://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\)). o tópico descreve como desinstalar uma versão específica e os procedimentos são semelhantes para versões anteriores.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  