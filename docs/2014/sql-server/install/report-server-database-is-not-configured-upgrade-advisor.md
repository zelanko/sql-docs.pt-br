---
title: O banco de dados do servidor de relatório não está configurado (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bb5dd5968930319532a29ff7c3909c36af99b3a0
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952115"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>O banco de dados do servidor de relatório não está configurado (Supervisor de Atualização)
  A atualização está bloqueada devido a uma configuração incompleta do servidor de relatório. O banco de dados do servidor de relatório não está configurado.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 A Instalação só pode atualizar uma instância do servidor de relatório completamente configurada. Para continuar, você deve configurar o banco de dados do servidor de relatório ou usar o **painel de controle** do Microsoft Windows para remover o recurso do servidor de relatório da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois de remover o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é possível atualizar outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Caso não tenha configurado o banco de dados do servidor de relatório, o servidor de relatório não estará operacional e deverá ser removido antes da atualização.  
  
 Para obter informações adicionais sobre a desinstalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [desinstalar o Reporting Services 2012](https://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\)). o tópico descreve como desinstalar uma versão específica e os procedimentos são semelhantes para versões anteriores.  
  
## <a name="see-also"></a>Consulte também  
 [Supervisor de atualização &#40;de problemas de atualização do Reporting Services&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
