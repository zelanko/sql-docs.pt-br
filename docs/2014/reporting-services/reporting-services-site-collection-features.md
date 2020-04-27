---
title: Reporting Services recursos do conjunto de sites | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9475ee323222b800a9c4b9a86e737fdd161e7a60
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102757"
---
# <a name="reporting-services-site-collection-features"></a>Recursos da coleção de sites do Reporting Services
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] O modo SharePoint fornece três recursos de coleção de sites do SharePoint. Os recursos dão suporte ao ambiente geral de relatório do modo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint, [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], um recurso do Suplemento [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para [!INCLUDE[SPS2010](../includes/sps2010-md.md)] Enterprise Edition, bem como a operações de gerenciamento para o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] na Administração Central do SharePoint.  
  
## <a name="site-collection-features"></a>Recursos da coleção de sites  
 A tabela a seguir descreve os membros da coleção de sites do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
|Recurso|Descrição|  
|-------------|-----------------|  
|**Recurso Administração Central do Servidor de Relatório**|Habilita recursos para o gerenciamento da integração com um servidor de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Esse recurso somente é instalado e usado na coleção de sites da Administração Central do SharePoint.<br /><br /> O recurso de integração do servidor de relatório é ativado automaticamente no conjunto de sites da administração central [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] do SharePoint depois que você instala o suplemento para produtos do SharePoint. Em algumas situações, você precisará ativar manualmente o recurso. Para ativar o recurso de servidor do relatório, use as páginas do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] na página Configurações de Site da Administração Central do SharePoint.<br /><br /> A versão [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e posteriores do Suplemento para produtos SharePoint ativarão o recurso de integração do servidor de relatório para todas as coleções de sites existentes quando o Suplemento for instalado. Além disso, o recurso ficará ativo automaticamente para novas coleções de sites.|  
|**Recurso de Integração do Servidor de Relatório**|Habilita relatórios avançados usando [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> Esse recurso está Ativo por padrão.|  
|**Recurso de Integração do Power View**|Permite a exploração de dados interativa e a apresentação visual em pastas de trabalho PowerPivot e Análise conserta bancos de dados de tabela do Analysis Services.<br /><br /> O recurso pode ser acessado pelos menus de contexto das seguintes fontes de dados:<br /><br /> .rdlx<br /><br /> .rsds<br /><br /> arquivo de conexão .bism<br /><br /> <br /><br /> Se [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] não aparecer nos menus de contexto, verifique se o **Recurso de Integração do Power View** está ativado.<br /><br /> Esse recurso está desativado por padrão.|  
  
## <a name="see-also"></a>Consulte Também  
 [Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Reporting Services configurações de site e recursos de site&#40;modo do SharePoint&#41;](../../2014/reporting-services/reporting-services-site-settings-and-site-features-sharepoint-mode.md)   
 [Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)  
  
  
