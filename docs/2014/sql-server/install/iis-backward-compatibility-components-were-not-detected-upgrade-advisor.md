---
title: Compatibilidade com versões anteriores do IIS componentes não foram detectados (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9cfae4d34ef825ac1781c90fda8d7e38c0299a1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094774"
---
# <a name="iis-backward-compatibility-components-were-not-detected-upgrade-advisor"></a>Componentes compatíveis com versões anteriores do IIS não detectados (Supervisor de Atualização)
  O Supervisor de Atualização não detecta componentes e configurações IIS que fornecem informações usadas pela Instalação para criar novas URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O IIS inclui componentes que fornecem informações sobre o servidor de relatório e os diretórios virtuais do Gerenciador de Relatórios. Esses componentes não estão instalados no computador do servidor de relatório. A atualização pode continuar, mas as URLs do servidor de relatório ou do Gerenciador de Relatórios não serão recriadas pela atualização.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Após a conclusão da atualização, use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para definir as URLs do servidor de relatório ou do Gerenciador de Relatórios. Use o Gerenciador do IIS para remover os diretórios virtuais que não são mais necessários.  
  
 Para obter mais informações, consulte [configurar uma URL &#40;Configuration Manager do SSRS&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
