---
title: "Iniciar o Construtor de Relat&#243;rios | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Construtor de Relatórios, inicialização"
  - "iniciando o Construtor de Relatórios"
  - "integração com o SharePoint [Reporting Services], inicialização do Construtor de Relatórios"
  - "iniciando o Construtor de Relatórios"
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
caps.latest.revision: 56
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 56
---
# Iniciar o Construtor de Relat&#243;rios
  O Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] é um ambiente de criação de relatórios autônomo. Com ele, você pode criar relatórios paginados e publicá-los no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado em modo nativo ou integrado do SharePoint.  
  
 A primeira vez que iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo integrado do SharePoint, você será solicitado a baixá-lo do Centro de Download da Microsoft. 
 
![report-builder-get-report-builder](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 Você ou um administrador também podem [instalar o Construtor de Relatórios no computador do Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=219138). Consulte "Instalar o Construtor de Relatórios com o Systems Manager Server" em [Instalar o Construtor de Relatórios](../../reporting-services/install-windows/install-report-builder.md) para obter mais detalhes.
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] não é instalado quando você instala o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]; é necessário baixá-lo e instalá-lo separadamente.  
  
 Quando você inicia o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] do portal da Web ou do site do SharePoint, se uma versão anterior do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] for aberta, contate o administrador, que poderá atualizar a versão no portal da Web ou no site do SharePoint.  
  
## Para iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
1.  No navegador da Web, digite a URL do servidor de relatório na barra de endereços. Por padrão, a URL é http://\<*servername*>/reports.  
  
2.  Na barra superior do portal da Web, selecione **Novo** > **Relatório Paginado**.  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     Na primeira vez, você será solicitado a [instalar o construtor de relatórios](../../reporting-services/install-windows/install-report-builder.md). 
  
     Após essa primeira vez, o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] é aberto e você pode criar ou abrir um relatório do servidor de relatório.  
  
## Para iniciar o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] no modo integrado do SharePoint  
  
1.  Navegue até o site do SharePoint que contém a biblioteca desejada.  
  
2.  Abra a biblioteca.  
  
3.  Clique em **Documentos**.  
  
4.  No menu **Novo Documento** , clique em **Relatório do Construtor de Relatórios**.  
  
     Na primeira vez, isso iniciará o Assistente do SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] . Consulte [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md) para obter mais detalhes.  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
     **Observação** Se o menu **Novo Documento** não listar **Relatório do Construtor de Relatórios**, **Modelo do Construtor de Relatórios**ou **Fonte de Dados de Relatório**, seus tipos de conteúdo precisarão ser adicionados à biblioteca do SharePoint. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
## Consulte também  
 [Construtor de Relatórios no SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Definir opções padrão para o Construtor de Relatórios](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  
  
  