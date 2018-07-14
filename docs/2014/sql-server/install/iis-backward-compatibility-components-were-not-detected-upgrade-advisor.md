---
title: Compatibilidade com versões anteriores do IIS componentes não foram detectados (Supervisor de atualização) | Microsoft Docs
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
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 689ca199202b594376a4d0785992123f6016e384
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177214"
---
# <a name="iis-backward-compatibility-components-were-not-detected-upgrade-advisor"></a>Componentes compatíveis com versões anteriores do IIS não detectados (Supervisor de Atualização)
  O Supervisor de Atualização não detecta componentes e configurações IIS que fornecem informações usadas pela Instalação para criar novas URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 O IIS inclui componentes que fornecem informações sobre o servidor de relatório e os diretórios virtuais do Gerenciador de Relatórios. Esses componentes não estão instalados no computador do servidor de relatório. A atualização pode continuar, mas as URLs do servidor de relatório ou do Gerenciador de Relatórios não serão recriadas pela atualização.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Após a conclusão da atualização, use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para definir as URLs do servidor de relatório ou do Gerenciador de Relatórios. Use o Gerenciador do IIS para remover os diretórios virtuais que não são mais necessários.  
  
 Para obter mais informações, consulte [configurar uma URL &#40;Configuration Manager do SSRS&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
