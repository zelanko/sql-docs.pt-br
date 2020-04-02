---
title: Iniciar o Construtor de Relatórios | Microsoft Docs
description: O Construtor de Relatórios é um ambiente de criação de relatórios autônomo. Na primeira vez em que você o inicia, o Centro de Download da Microsoft solicita que você o baixe.
ms.date: 01/03/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bdb67ef174ec849233826b65a2d90f08e8e4eb7d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80290768"
---
# <a name="start-report-builder"></a>Iniciar o Construtor de Relatórios

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] é um ambiente de criação de relatórios autônomo. Com ele, você pode criar relatórios paginados e publicá-los no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado em modo nativo ou integrado do SharePoint.  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
 Na primeira vez que você iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo integrado do SharePoint, será solicitado que você o baixe do Centro de Download da Microsoft. 
 
![report-builder-get-report-builder](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 Você ou um administrador também podem [instalar o Construtor de Relatórios no computador do Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?LinkID=219138). Consulte "Instalar o Construtor de Relatórios com o Systems Manager Server" em [Instalar o Construtor de Relatórios](../../reporting-services/install-windows/install-report-builder.md) para obter mais detalhes.
 
 O [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] não é instalado quando você instala o SQL Server Reporting Services; você precisa baixar e instalá-lo separadamente.  
  
 Quando você inicia o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] do portal da Web ou do site do SharePoint, se uma versão anterior do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] for aberta, contate o administrador, que poderá atualizar a versão no portal da Web ou no site do SharePoint.  
  
## <a name="to-start-ssrbnoversion-from-the-ssrsnoversion-web-portal"></a>Para iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
1.  No navegador da Web, digite a URL do servidor de relatório na barra de endereços. Por padrão, a URL é https://\<*nomedoservidor*>/reports.  
  
2.  Na barra superior do portal da Web, selecione **Novo** > **Relatório Paginado**.  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     Na primeira vez, você será solicitado a [instalar o construtor de relatórios](../../reporting-services/install-windows/install-report-builder.md). 
  
     Após essa primeira vez, o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] é aberto e você pode criar ou abrir um relatório do servidor de relatório.  
  
## <a name="to-start-ssrbnoversion-in-sharepoint-integrated-mode"></a>Para iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] no modo integrado do SharePoint  
  
1.  Navegue até o site do SharePoint que contém a biblioteca desejada.  
  
2.  Abra a biblioteca.  
  
3.  Clique em **Documentos**.  
  
4.  No menu **Novo Documento** , clique em **Relatório do Construtor de Relatórios**.  
  
     Na primeira vez, isso iniciará o Assistente do SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. Consulte [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md) para obter mais detalhes.  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
     **Observação** Se o menu **Novo Documento** não listar **Relatório do Construtor de Relatórios**, **Modelo do Construtor de Relatórios**ou **Fonte de Dados de Relatório**, seus tipos de conteúdo precisarão ser adicionados à biblioteca do SharePoint. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  

## <a name="next-steps"></a>Próximas etapas

[Construtor de Relatórios no SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
[Definir opções padrão para o Construtor de Relatórios](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
