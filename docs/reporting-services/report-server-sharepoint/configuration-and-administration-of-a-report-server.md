---
title: "Configuração e administração de um servidor de relatório do SQL Server Reporting Services | Microsoft Docs"
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
ms.workload: Inactive
ms.openlocfilehash: fe898a9401340f80884fa15f3ea1ce45108fbbc6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="configuration-and-administration-of-a-sql-server-reporting-services-report-server"></a>Configuração e administração de um servidor de relatório do SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

O SQL Server Reporting Services é uma plataforma de relatório com base em servidor que fornece uma ampla gama de ferramentas e serviços prontos para uso, para ajudá-lo a criar, implantar e gerenciar relatórios para a sua organização, além de recursos de programação que lhe permitem estender e personalizar suas funções de relatório. Você pode integrar seu ambiente de relatório com um produto do SharePoint para experimentar os benefícios de usar o ambiente de colaboração fornecidos por sites do SharePoint.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

Use as seguintes seções para ajudá-lo a entender conceitos, cenários de implantação, procedimentos e muito mais para integrar seu ambiente do Reporting Services a um produto ou tecnologia do SharePoint:  
  
-   Opções de menu em uma biblioteca do SharePoint  
  
    -   [Gerenciador de Alertas de Dados para Usuários do SharePoint](../../reporting-services/data-alert-manager-for-sharepoint-users.md)  
  
    -   [Criar e gerenciar assinaturas de servidores de relatório no modo SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
    -   [Atualizar credenciais em fontes de dados de relatório de um site do SharePoint](../../reporting-services/report-data/update-credentials-in-report-data-sources-from-a-sharepoint-site.md)  
  
    -   [Gerenciar conjuntos de dados compartilhados](../../reporting-services/report-data/manage-shared-datasets.md)  
  
    -   [Definir parâmetros em um relatório publicado &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)  
  
    -   [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
    -   [Opções de atualização do cache &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6)  
  
-   [Recursos da coleção de sites do Reporting Services](../../reporting-services/report-server-sharepoint/site-collection-features-reporting-services.md)  
  
-   [Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)  
  
-   [Configurações de Site e Recursos de Site do Reporting Services &#40;Modo SharePoint&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)  
  
-   [Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  
  
-   [Adicionar os tipos de conteúdo do Reporting Services a uma biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
-   [Relatórios em Modo Local versus em modo Conectado no Visualizador de Relatórios &#40;Reporting Services no modo do SharePoint&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
-   [Carregar documentos em uma biblioteca do SharePoint &#40;Reporting Services no modo do SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
-   [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
 Para obter informações mais gerais sobre o Reporting Services, consulte [Reporting Services](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre outros componentes, ferramentas e recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte os [Manuais Online do SQL Server.](../../sql-server/sql-server-technical-documentation.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
