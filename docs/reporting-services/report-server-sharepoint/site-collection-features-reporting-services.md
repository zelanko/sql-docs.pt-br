---
title: "Recursos do Reporting Services site coleção | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 7c86f9ecdbbf4955ba224e40c245fc412742fc30
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="reporting-services-site-collection-features"></a>Recursos do conjunto de site do Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Modo do Reporting Services SharePoint fornece três recursos de coleção de sites do SharePoint. Os recursos de suporte ao modo SharePoint do Reporting Services geral reporting ambiente, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], um recurso do SQL Server 2016 Reporting Services Add-in e operações de gerenciamento para o Reporting Services na Administração Central do SharePoint.

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.
  
## <a name="site-collection-features"></a>Recursos do conjunto de sites

 A tabela a seguir descreve os recursos de coleta de site do Reporting Services.  
  
|Recurso|Description|  
|-------------|-----------------|  
|**Recurso Administração Central do Servidor de Relatório**|Habilita recursos para gerenciar a integração com um servidor de relatório do Reporting Services. Esse recurso somente é instalado e usado na coleção de sites da Administração Central do SharePoint.<br /><br /> O recurso de integração do Servidor de Relatório é ativado automaticamente na coleção de sites da Administração Central do SharePoint depois que você instala o Suplemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para produtos SharePoint. Em algumas situações, você precisa ativar manualmente o recurso. Para ativar o recurso de servidor de relatório, use as páginas do Reporting Services na página de configurações do Site de Administração Central SharePoint.<br /><br /> O [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] versão do Reporting Services e posterior do suplemento para SharePoint produtos ativar o recurso de integração do servidor de relatório para todos os conjuntos de sites existentes quando o suplemento está instalado. Além disso, o recurso está ativo automaticamente para novos conjuntos de sites.|  
|**Recurso de Integração do Servidor de Relatório**|Permite relatórios ricos usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Reporting Services<br /><br /> Esse recurso está Ativo por padrão.|  
|**Recurso de Integração do Power View**|Habilita a exploração de dados interativa e a apresentação visual em pastas de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , bem como bancos de dados de tabela do Analysis.Services.<br /><br /> O recurso pode ser acessado pelos menus de contexto das seguintes fontes de dados:<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> Arquivo de conexão**.bism** <br /><br /> <br /><br /> Se [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] não aparecer nos menus de contexto, verifique se o **Recurso de Integração do Power View** está ativado.<br /><br /> Esse recurso está desativado por padrão.|  

## <a name="next-steps"></a>Próximas etapas

[Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Configurações de Site e Recursos de Site do Reporting Services &#40;Modo SharePoint&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
