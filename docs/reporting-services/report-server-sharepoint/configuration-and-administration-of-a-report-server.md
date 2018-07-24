---
title: Configuração e administração de um servidor de relatório (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7959539dde52351bc9679b9b4629e2d1a4105562
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38049134"
---
# <a name="configuration-and-administration-of-a-sql-server-reporting-services-ssrs-report-server"></a>Configuração e administração de um servidor de relatório do SSRS (SQL Server Reporting Services)

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
