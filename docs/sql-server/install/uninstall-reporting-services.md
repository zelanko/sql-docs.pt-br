---
title: Desinstalar o Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5c764a00-d4bc-465d-b32e-e4efce052ce4
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: be3ac5ed46a8807d6d78296d142ae36b9eb7664d
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="uninstall-reporting-services"></a>Desinstalar o Reporting Services
  A desinstalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não remove o conteúdo que você criou ou a configuração que você modificou. Porém, se algum conteúdo precisar ser utilizado depois que a desinstalação for concluída, é recomendável fazer cópias do conteúdo antes de começar o processo de desinstalação.  
  
## <a name="uninstall-sharepoint-mode"></a>Desinstalar o modo do SharePoint  
 Ao desinstalar o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , os seguintes componentes são removidos:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e proxy de serviço.  
  
-   Arquivos usados na instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Os aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não são removidos. Se você não quiser mais os aplicativos de serviço, exclua-os usando o Windows PowerShell ou a Administração Central do SharePoint.  
  
 Os itens de relatório e metadados relacionados não são removidos. Essas informações encontram-se nos bancos de dados de conteúdo e configuração relacionados aos aplicativos de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Os bancos de dados não são removidos e você pode migrá-los manualmente para outra instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint. Se você não quiser mais as informações, exclua os bancos de dados. Para obter mais informações, consulte [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 A seguir são apresentados nomes de exemplo dos três bancos de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que não são removidos.  
  
-   **Banco de dados do servidor de relatório:** ReportingService_7f616e2d253040e8ab5653b3c09a065e  
  
-   **Banco de dados temporário do servidor de relatório:** ReportingService_7f616e2d253040e8ab5653b3c09a065eTempDB  
  
-   **Banco de dados de alertas do servidor de relatório:** ReportingService_7f616e2d253040e8ab5653b3c09a065e_Alerting  
  
### <a name="uninstall-the-add-in-for-sharepoint-products"></a>Desinstale o suplemento para produtos do SharePoint.  
 Ao desinstalar o suplemento de um computador, você pode optar por desinstalar somente os arquivos ou também para remover o recursos [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do farm. Para obter informações sobre como instalar o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para os produtos do SharePoint, veja [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
## <a name="uninstall-native-mode"></a>Desinstalar o modo nativo  
 Quando você desinstala o modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , qualquer coisa que tiver sido **criada** ou **modificada** depois da instalação é deixada no local. Por exemplo, arquivos de banco de dados, arquivos de log, arquivos de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e itens de conteúdo, como relatórios e arquivos de fonte de dados.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é um recurso de instância e, portanto, não está listado no Painel de Controle do Windows, em Programas e Recursos. Para desinstalar o modo Nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
1.  No Painel de Controle do Windows, clique em **Programas e Recursos**.  
  
2.  Em **Programas e Recursos** , selecione **Microsoft SQL Server 2012**.  
  
3.  No assistente de desinstalação, selecione a instância que inclui o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] recurso de instância **RS** do.  
  
     ![rs_nativemode_uninstall_selectinstance](../../sql-server/install/media/rs-nativemode-uninstall-selectinstance.gif "rs_nativemode_uninstall_selectinstance")  
  
4.  Depois que você selecionar a instância, selecione o recurso do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![rs_nativemode_uninstall_selectfeatures](../../sql-server/install/media/rs-nativemode-uninstall-selectfeatures.gif "rs_nativemode_uninstall_selectfeatures")  
  
5.  Conclua o assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Desinstalar uma instância existente do SQL Server &#40;instalação&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
