---
title: "Recursos de coleção do Site do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b68204ab4c9a008db7c43d2c568d1c3ccedbcb7a
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---

# <a name="site-collection-features---reporting-services"></a>Recursos de coleção do site - Reporting Services

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O modo SharePoint fornece três recursos de coleção de sites do SharePoint. Os recursos de suportam geral [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint do reporting ambiente, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], um recurso do SQL Server 2016 Reporting Services Add-in e operações de gerenciamento para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na Administração Central do SharePoint.  
  
## <a name="site-collection-features"></a>Recursos da coleção de sites  
 A tabela a seguir descreve os membros da coleção de sites do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|Recurso|Description|  
|-------------|-----------------|  
|**Recurso Administração Central do Servidor de Relatório**|Habilita recursos para o gerenciamento da integração com um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Esse recurso somente é instalado e usado na coleção de sites da Administração Central do SharePoint.<br /><br /> O recurso de integração do Servidor de Relatório é ativado automaticamente na coleção de sites da Administração Central do SharePoint depois que você instala o Suplemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para produtos SharePoint. Em algumas situações, você precisará ativar manualmente o recurso. Para ativar o recurso de servidor do relatório, use as páginas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na página Configurações de Site da Administração Central do SharePoint.<br /><br /> A versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e posteriores do Suplemento para produtos SharePoint ativarão o recurso de integração do servidor de relatório para todas as coleções de sites existentes quando o Suplemento for instalado. Além disso, o recurso ficará ativo automaticamente para novas coleções de sites.|  
|**Recurso de Integração do Servidor de Relatório**|Habilita relatórios avançados usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]<br /><br /> Esse recurso está Ativo por padrão.|  
|**Recurso de Integração do Power View**|Habilita a exploração de dados interativa e a apresentação visual em pastas de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , bem como bancos de dados de tabela do Analysis.Services.<br /><br /> O recurso pode ser acessado pelos menus de contexto das seguintes fontes de dados:<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> Arquivo de conexão**.bism** <br /><br /> <br /><br /> Se [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] não aparecer nos menus de contexto, verifique se o **Recurso de Integração do Power View** está ativado.<br /><br /> Esse recurso está desativado por padrão.|  

## <a name="next-steps"></a>Próximas etapas

[Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Configurações de Site e Recursos de Site do Reporting Services &#40;Modo SharePoint&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
