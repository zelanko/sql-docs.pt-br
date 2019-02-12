---
title: Conectar-se o filtro ou uma Web Part de documentos (Reporting Services no modo integrado do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 4da46abbfb586a2968f92a04538f5a82e06898c6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031217"
---
# <a name="connect-filter-or-documents-web-part-reporting-services-in-sharepoint-integrated-mode"></a>Conectar Web Part de filtro ou de documentos (Reporting Services no modo integrado do SharePoint)
  Se estiver usando um produto do SharePoint, você poderá criar um painel ou Página de Web Part que inclua uma Web Part de filtro ou de documentos e uma Web Part do Visualizador de Relatórios. As versões com suporte são [!INCLUDE[SPF2010](../includes/spf2010-md.md)] ou [!INCLUDE[SPS2010](../includes/sps2010-md.md)]. Também há suporte para [!INCLUDE[winSPServ3](../includes/winspserv3-md.md)] ou [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007. Ao conectarem uma Web Part de filtro, os usuários que selecionam valores de filtro em uma Web Part de filtro podem enviar o valor para um relatório parametrizado na mesma página. Ao conectarem uma Web Part de documento, os usuários que clicarem na biblioteca de Documentos podem exibir o relatório em uma Web Part do Visualizador de Relatórios adjacente.  
  
 A Web Part de filtro é usada para enviar valores a um ou mais parâmetros em um relatório. Para usar uma Web Part de filtro, o relatório deve ter parâmetros definidos para ele, compatíveis com os valores, o tipo de dados e o formato enviado pela Web Part.  
  
 A Web Part de documento é associada à biblioteca de Documentos do site Inicial. Para exibir, adicionar ou remover itens na Biblioteca de Documentos, clique em **Exibir Todo o Conteúdo do Site**. Em Bibliotecas, clique em **Documentos**. Você pode usar os menus **Novo**, **Carregar**e **Ações** para gerenciar os itens da Biblioteca de Documentos.  
  
### <a name="to-connect-a-filter-web-part"></a>Para conectar uma Web Part de filtro  
  
1.  Abra ou crie uma página ou um painel da Web Part.  
  
2.  No menu **Ações do Site** , clique em **Editar Página**.  
  
3.  Clique em **Adicionar uma Web Part**.  
  
4.  Em **Todas as Web Parts**, na categoria **Diversos** , selecione **Visualizador de Relatórios do SQL Server Reporting Services**.  
  
5.  Clique em **Adicionar**. A Web Part será adicionada à parte superior da zona.  
  
6.  Em outra zona da mesma página ou do mesmo painel da Web Part, clique em **Adicionar uma Web Part**.  
  
7.  Em **Todas as Web Parts**, na seção **Filtros** , selecione uma Web Part.  
  
8.  Clique em **Adicionar**. A Web Part será adicionada à parte superior da zona.  
  
9. Na zona que contém a Web Part, clique no menu **Editar** da Web Part, aponte para **Conexões**, para **Enviar Valores de Filtro Para**e selecione **Visualizador de Relatórios** - *nome do relatório*.  
  
10. Verifique suas alterações e salve a página.  
  
### <a name="to-connect-a-documents-web-part"></a>Para conectar uma Web Part de documento  
  
1.  Abra ou crie uma página ou um painel da Web Part.  
  
2.  No menu **Ações do Site** , clique em **Editar Página**.  
  
3.  Clique em **Adicionar uma Web Part**.  
  
4.  Em **Todas as Web Parts**, na seção **Listas e Biblioteca** , selecione **Documentos**.  
  
5.  Clique em **Adicionar**. A Web Part será adicionada à parte superior da zona.  
  
6.  Clique em **Aplicar** na parte inferior do painel de ferramentas e clique em **OK** para fechar esse painel.  
  
7.  Em outra zona da mesma página ou do mesmo painel da Web Part, clique em **Adicionar uma Web Part**.  
  
8.  Em **Todas as Web Parts**, na categoria **Diversos** , selecione **Visualizador de Relatórios do SQL Server Reporting Services.**  
  
9. Clique em **Adicionar**. A Web Part será adicionada à parte superior da zona.  
  
10. Na zona que contém a Web Part, clique no menu **Editar** da Web Part, aponte para **Conexões**, para **Obter definições de relatório de**e selecione **Documentos**.  
  
11. Verifique suas alterações e salve a página.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar a Web Part do Visualizador de Relatórios a uma página da Web &#40;Reporting Services no modo integrado do SharePoint&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [Web Part do Visualizador de Relatórios em um site do SharePoint](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar a Web Part do Visualizador de Relatórios](../../2014/reporting-services/customize-the-report-viewer-web-part.md)  
  
  
