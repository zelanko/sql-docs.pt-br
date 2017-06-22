---
title: "Iniciar o construtor de relatórios | Microsoft Docs"
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
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
caps.latest.revision: 56
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e99d13a8e80a0ed2a5e584dcc0e20591507f8c92
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---

# <a name="start-report-builder"></a>Iniciar o Construtor de Relatórios

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]é um relatório autônomo ambiente de criação. Com ele, você pode criar relatórios paginados e publicá-los no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado em modo nativo ou integrado do SharePoint.  
  
 A primeira vez que iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo integrado do SharePoint, você será solicitado a baixá-lo do Centro de Download da Microsoft. 
 
![report-builder-get-report-builder](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 Você ou um administrador também podem [instalar o Construtor de Relatórios no computador do Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=219138). Consulte "Instalar o Construtor de Relatórios com o Systems Manager Server" em [Instalar o Construtor de Relatórios](../../reporting-services/install-windows/install-report-builder.md) para obter mais detalhes.
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]não é instalado quando você instala o SQL Server Reporting Services; Você precisa baixar e instalá-lo separadamente.  
  
 Quando você inicia o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] do portal da Web ou do site do SharePoint, se uma versão anterior do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] for aberta, contate o administrador, que poderá atualizar a versão no portal da Web ou no site do SharePoint.  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversion-mdmd-from-the-includessrsnoversionincludesssrsnoversion-mdmd-web-portal"></a>Para iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
1.  No navegador da Web, digite a URL do servidor de relatório na barra de endereços. Por padrão, a URL é http://\<*servername*> / reports.  
  
2.  Na barra superior do portal da Web, selecione **Novo** > **Relatório Paginado**.  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     Na primeira vez, você será solicitado a [instalar o construtor de relatórios](../../reporting-services/install-windows/install-report-builder.md). 
  
     Após essa primeira vez, o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] é aberto e você pode criar ou abrir um relatório do servidor de relatório.  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversion-mdmd-in-sharepoint-integrated-mode"></a>Para iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] no modo integrado do SharePoint  
  
1.  Navegue até o site do SharePoint que contém a biblioteca desejada.  
  
2.  Abra a biblioteca.  
  
3.  Clique em **Documentos**.  
  
4.  No menu **Novo Documento** , clique em **Relatório do Construtor de Relatórios**.  
  
     Na primeira vez, isso iniciará o Assistente do SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] . Consulte [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md) para obter mais detalhes.  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
     **Observação** Se o menu **Novo Documento** não listar **Relatório do Construtor de Relatórios**, **Modelo do Construtor de Relatórios**ou **Fonte de Dados de Relatório**, seus tipos de conteúdo precisarão ser adicionados à biblioteca do SharePoint. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  

## <a name="next-steps"></a>Próximas etapas

[Construtor de Relatórios no SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
[Definir opções padrão para o construtor de relatórios](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
