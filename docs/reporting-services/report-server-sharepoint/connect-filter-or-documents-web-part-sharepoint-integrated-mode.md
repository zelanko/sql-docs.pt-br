---
title: "Conectar web part de filtro ou documentos com uma web part do Visualizador de relatórios do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
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
ms.openlocfilehash: 87d4b4a3f0c01804329f3a7b0688632c20ed6c9b
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>Conectar web part de filtro ou documentos com uma web part do Visualizador de relatórios do Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Se você estiver usando um produto do SharePoint, você pode criar um painel ou a web part página que inclua uma web part de filtro ou web part de documentos e uma web part do Visualizador de relatórios. As versões com suporte são [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]. Também há suporte para [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] ou [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007. Ao conectar uma web part de filtro, os usuários que selecionam valores de filtro em uma web part de filtro podem enviar o valor para um relatório parametrizado na mesma página. Conectando uma web part de documentos, os usuários que clicarem na biblioteca de documentos podem exibir o relatório em uma web part do Visualizador de relatórios adjacente.

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

 A web part de filtro é usado para enviar valores para um ou mais parâmetros em um relatório. Para usar uma web part de filtro, o relatório deve ter parâmetros definidos para ele e que são compatíveis com os valores, o tipo de dados e o formato enviado pela web part.  
  
 A web part de documentos é associada à biblioteca de documentos do site inicial. Para exibir, adicionar ou remover itens na Biblioteca de Documentos, clique em **Exibir Todo o Conteúdo do Site**. Em Bibliotecas, clique em **Documentos**. Você pode usar os menus **Novo**, **Carregar**e **Ações** para gerenciar os itens da Biblioteca de Documentos.  
  
## <a name="connect-a-filter-web-part"></a>Conectar uma web part de filtro
  
1.  Abra ou crie a página de web part ou um painel.  
  
2.  No menu **Ações do Site** , clique em **Editar Página**.  
  
3.  Clique em **adicionar uma web part**.  
  
4.  Em **todas as web parts**, além de **diversos** categoria, selecione **Visualizador de relatórios do SQL Server Reporting Services**.  
  
5.  Clique em **Adicionar**. A web part será adicionada na parte superior da zona.  
  
6.  Em outra zona da mesma página de web Parts ou painel, clique em **adicionar uma web part**.  
  
7.  Em **todas as web parts**, no **filtros** seção, selecione uma web part.  
  
8.  Clique em **Adicionar**. A web part será adicionada na parte superior da zona.  
  
9. Na zona que contém a web part, clique na web part **editar** , aponte para **conexões**, aponte para **enviar valores de filtro para**e, em seguida, selecione **relatório Visualizador** - *nome do relatório*.  
  
10. Verifique suas alterações e salve a página.  
  
## <a name="connect-a-documents-web-part"></a>Conectar uma web part de documentos  
  
1.  Abra ou crie a página de web part ou um painel.  
  
2.  No menu **Ações do Site** , clique em **Editar Página**.  
  
3.  Clique em **adicionar uma web part**.  
  
4.  Em **todas as web parts**, além de **listas e biblioteca** seção, selecione **documentos.**  
  
5.  Clique em **Adicionar**. A web part será adicionada na parte superior da zona.  
  
6.  Clique em **Aplicar** na parte inferior do painel de ferramentas e clique em **OK** para fechar esse painel.  
  
7.  Em outra zona da mesma página de web Parts ou painel, clique em **adicionar uma web part**.  
  
8.  Em **todas as web parts**, além de **diversos** categoria, selecione **Visualizador de relatórios do SQL Server Reporting Services.**  
  
9. Clique em **Adicionar**. A web part será adicionada na parte superior da zona.  
  
10. Na zona que contém a web part, clique na web part **editar** , aponte para **conexões**, aponte para **obter definições de relatório de**e, em seguida, selecione  **Documentos**.  
  
11. Verifique suas alterações e salve a página.  
  
## <a name="see-also"></a>Consulte também

 [Adicionar a web part do Visualizador de relatórios para uma página da web](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [Web part do Visualizador de relatórios em um Site do SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar a Web Part do Visualizador de Relatórios](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
