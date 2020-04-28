---
title: Os componentes de compatibilidade com versões anteriores do IIS não foram detectados (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: dbf5686d4a947cb8629675368c59c8039c93835e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952500"
---
# <a name="iis-backward-compatibility-components-were-not-detected-upgrade-advisor"></a>Componentes compatíveis com versões anteriores do IIS não detectados (Supervisor de Atualização)
  O Supervisor de Atualização não detecta componentes e configurações IIS que fornecem informações usadas pela Instalação para criar novas URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O IIS inclui componentes que fornecem informações sobre o servidor de relatório e os diretórios virtuais do Gerenciador de Relatórios. Esses componentes não estão instalados no computador do servidor de relatório. A atualização pode continuar, mas as URLs do servidor de relatório ou do Gerenciador de Relatórios não serão recriadas pela atualização.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Após a conclusão da atualização, use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para definir as URLs do servidor de relatório ou do Gerenciador de Relatórios. Use o Gerenciador do IIS para remover os diretórios virtuais que não são mais necessários.  
  
 Para obter mais informações, consulte [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) nos manuais online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Reporting Services &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
