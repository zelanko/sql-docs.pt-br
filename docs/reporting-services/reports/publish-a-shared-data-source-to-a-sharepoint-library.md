---
title: "Publicar uma fonte de dados compartilhada em uma biblioteca do SharePoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "fontes de dados [Reporting Services], publicando em uma biblioteca do SharePoint"
  - "Integração do SharePoint [Reporting Services], publicando em uma biblioteca"
  - "publicando relatórios [Reporting Services], em uma biblioteca do SharePoint"
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 14
---
# Publicar uma fonte de dados compartilhada em uma biblioteca do SharePoint
  Para publicar uma fonte de dados compartilhada em um servidor de relatório executado no modo integrado SharePoint, defina as propriedades do projeto de relatório no Designer de Relatórios. Nas propriedades do projeto, todas as referências a servidores, relatórios e fontes de dados compartilhadas devem ser URLs totalmente qualificadas.  
  
 Você deve ter permissão de **Membro** ou **Proprietário** no site do SharePoint. Para obter mais informações, consulte [Exemplos de URL para itens de relatório publicados em um servidor de relatório em modo de SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### Para publicar uma fonte de dados compartilhada em um site do SharePoint  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um projeto do Servidor de Relatório existente ou novo.  
  
2.  No menu **Projeto** , clique em **Propriedades**. A caixa de diálogo **Páginas de Propriedade** de *\<project>* será aberta.  
  
3.  Escolha a **Configuração** que deseja usar para publicar no site do SharePoint.  
  
4.  Para publicar fontes de dados compartilhadas no seu projeto e substituir as fontes de dados compartilhadas publicadas, defina **OverwriteDataSources** como **True**.  
  
5.  (Opcional) Para **TargetDataSourceFolder**, digite uma URL em uma biblioteca do SharePoint ou pasta de biblioteca. Por exemplo, *http://TestServer/TestSite/Documents/DataSources*.  
  
     Se você não especificar um valor, o valor **TargetReportFolder** será usado.  
  
6.  Para **TargetReportFolder**, digite uma URL em uma biblioteca ou pasta de biblioteca. Por exemplo, http:*//TestServer/TestSite/Documents/Reports*.  
  
7.  Para **TargetServerURL**, digite uma URL em um site de nível superior ou subsite do SharePoint. Se você não especificar um site, o site padrão de nível superior será usado. Por exemplo, http://*nome_do_servidor*, http://*nome_do_servidor*/*site* ou http://*nome_do_servidor*/*site*/*subsite*.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. No Gerenciador de Soluções, clique com o botão direito do mouse na fonte de dados compartilhada que você deseja publicar e, em seguida, clique em **Implantar**. A fonte de dados será publicada no local especificado em **TargetDataSourceFolder**. Erros de implantação são exibidos na janela Saída.  
  
    > [!NOTE]  
    >  Após a publicação de uma fonte de dados compartilhada em um site do SharePoint, a extensão de nome de arquivo será alterada para .rsds. Você pode editar e gerenciar uma fonte de dados compartilhada diretamente no site do SharePoint. Para obter mais informações, consulte [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md).  
  
## Consulte também  
 [Publicar um relatório em uma biblioteca do SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Exemplos de URL para itens de relatório publicados em um Servidor de Relatório no modo do SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Caixa de diálogo Páginas de Propriedades do Projeto](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Definir propriedades de implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [Publicando relatórios em um servidor de relatórios](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [Usar uma conexão de dados do Office &#40;.odc&#41; com relatórios &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-data/use an office data connection (.odc) with reports.md)  
  
  