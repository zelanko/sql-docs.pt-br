---
title: Adicionar tipos de conteúdo de servidor de relatório a uma biblioteca (Reporting Services no modo integrado do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ac9136c8-9ef4-484c-8e9d-05008a186db5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 50ff2626108c26ca5cee3845da437b27dbfcade0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030847"
---
# <a name="add-report-server-content-types-to-a-library-reporting-services-in-sharepoint-integrated-mode"></a>Adicionar tipos de conteúdo do servidor de relatório a uma biblioteca (Reporting Services no modo integrado do SharePoint)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece tipos de conteúdo predefinidos do SharePoint usados para gerenciar arquivos de fonte de dados compartilhada (.rsds), modelos de relatórios (.smdl) e arquivos de definição de relatório (.rdl) do Construtor de Relatórios. A adição de um tipo de conteúdo do **Construtor de Relatórios**, do **Modelo de Relatório**ou da **Fonte de Dados de Relatório** a uma biblioteca ativa o comando **Novo** para que você possa criar novos documentos desse tipo.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Modo do SharePoint  
  
 Para adicionar tipos de conteúdo a uma biblioteca, é necessário que você seja administrador de site ou ter o nível de permissão Controle Total.  
  
 Os tipos de conteúdo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e o gerenciamento de tipo de conteúdo serão automaticamente habilitados em todas as bibliotecas de documentos para conjuntos de sites existentes criados no modelo de site da **Central de Business Intelligence** .  
  
 Sites criados depois da integração do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não terão os tipos de conteúdo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] habilitados.  
  
> [!TIP]  
>  Se você **não** tiver configurado anteriormente tipos de conteúdo para uma biblioteca, primeiro habilite o gerenciamento de tipos de conteúdo e, depois, habilite os tipos de conteúdo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Consulte os procedimentos para habilitar o gerenciamento de tipo de conteúdo em uma única biblioteca de documentos.  
  
 **Vídeo curto:** [(SSRS) Habilitar tipos de conteúdo em SharePoint2010.wmv](http://www.youtube.com/watch?v=yqhm3DrtT1w) (http://www.youtube.com/watch?v=yqhm3DrtT1w).  
  
 **Neste tópico:**  
  
-   [Habilitar tipos de conteúdo em todas as bibliotecas de documentos em um centro de BI existente](#bkmk_enable_all)  
  
-   [Para habilitar o gerenciamento de tipo de conteúdo para uma única biblioteca de documentos (SharePoint 2013)](#bkmk_enable_content_management)  
  
-   [Para adicionar tipos de conteúdo do Reporting Services (SharePoint 2013)](#bkmk_add_single)  
  
-   [Para habilitar o gerenciamento de tipo de conteúdo para uma única biblioteca de documentos (SharePoint 2010)](#bkmk_enable_content_management_2010)  
  
-   [Para adicionar tipos de conteúdo de servidor de relatório (SharePoint 2010)](#bkmk_add_single_2010)  
  
-   [Para habilitar tipos de conteúdo e gerenciamento de conteúdo para vários sites de BI](#bkmk_enable_multiple_sites)  
  
##  <a name="bkmk_enable_all"></a> Habilitar tipos de conteúdo em todas as bibliotecas de documentos em um centro de BI existente  
  
1.  Para habilitar os tipos de conteúdo e o gerenciamento de conteúdo em todas as bibliotecas de documentos em um site existente da **Central de Business Intelligence** , você pode alternar o recurso de integração do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
2.  Vá para **Configurações de site**.  
  
    -   No SharePoint 2013, clique no ícone **Configurações** . ![Configurações do SharePoint](../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Settings")  
  
    -   No SharePoint 2010, clique em **Ações do Site**e, depois, em **Configurações de Site**.  
  
3.  Clique em **Recursos do conjunto de sites**.  
  
4.  Localize o **Recurso de Integração do Servidor de Relatório** e clique em **Desativar**.  
  
     ![rs_reportserver_integration_active](media/rs-reportserver-integration-active.gif "rs_reportserver_integration_active")  
  
5.  Atualize o navegador e clique em **Ativar** para o **Recurso de Integração do Servidor de Relatório**.  
  
    ![Deactivate](media/rs-reportserver-integration-deactivate.gif "rs_reportserver_integration_deactive")  
  
##  <a name="bkmk_enable_content_management"></a> Para habilitar o gerenciamento de tipo de conteúdo para uma única biblioteca de documentos (SharePoint 2013)  
  
1.  Abra a biblioteca para a qual você deseja habilitar vários tipos de conteúdo.  
  
2.  Clique em **Biblioteca** na faixa de opções.  
  
     ![rs_SharePoint2013_LibraryRibbon](media/rs-sharepoint2013-libraryribbon.gif "rs_SharePoint2013_LibraryRibbon")  
  
3.  Na faixa de opções **Biblioteca** , clique em **Configurações da Biblioteca**. Se não aparecer **Configurações da Biblioteca** ou se o botão estiver desabilitado, você não terá permissão para definir configurações da biblioteca, inclusive tipos de conteúdo.  
  
     ![rs_SharePoint2013_LibrarySettings](media/rs-sharepoint2013-librarysettings.gif "rs_SharePoint2013_LibrarySettings")  
  
4.  Na seção **Configurações Gerais** , clique em **Configurações avançadas**.  
  
     ![rs_SharePoint2013_LibrarySettings_AdvancedSettings](media/rs-sharepoint2013-librarysettings-advancedsettings.gif "rs_SharePoint2013_LibrarySettings_AdvancedSettings")  
  
5.  Na seção **Tipos de Conteúdo** , selecione **Sim** para permitir o gerenciamento de tipos de conteúdo.  
  
6.  Clique em **OK**.  
  
##  <a name="bkmk_add_single"></a> Para adicionar tipos de conteúdo do Reporting Services (SharePoint 2013)  
  
1.  Abra a biblioteca para a qual você deseja adicionar tipos de conteúdo do Reporting Services.  
  
2.  Na faixa de opções, clique em **Biblioteca**.  
  
3.  Clique em **Configurações da Biblioteca**.  
  
4.  Em **Tipos de Conteúdo**, clique em **Adicionar a partir de tipos de conteúdo de site existentes**.  
  
5.  Em **Selecionar tipos de conteúdo de site de**, selecione **Tipos de Conteúdo do SQL Server Reporting Services**.  
  
6.  Na lista **Tipos Disponíveis de Conteúdo do Site** , clique em **Construtor de Relatórios**e em **Adicionar** para mover o tipo de conteúdo selecionado para a lista **Tipos de conteúdo a serem adicionados** .  
  
7.  Para adicionar os tipos de conteúdo **Modelo de Relatório** e **Fonte de Dados do Relatório** , repita a etapa anterior.  
  
8.  Quando terminar de adicionar tipos de conteúdo, clique em **OK**.  
  
9. > [!NOTE]  
    >  Se o grupo de tipos de conteúdo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] **Tipos de Conteúdo do SQL Server Reporting Services** não estiver visível na página **Adicionar Tipos de Conteúdo** , uma das seguintes condições será verdadeira:  
  
    -   O suplemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para produtos do SharePoint não foi instalado. Para obter mais informações, consulte [instalar ou desinstalar o suplemento Reporting Services para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). O tópico inclui informações sobre a instalação do suplemento e apresenta as etapa de instalação somente de arquivos do suplemento para oferecer soluções alternativas.  
  
    -   O suplemento está instalado, mas o recurso de coleta de site **Recurso de Integração do Servidor de Relatório** não está ativo. Confirme o recurso de coleta de site em **Configurações do Site**.  
  
    -   Todos os tipos de conteúdo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] já foram adicionados à biblioteca. Se todos os tipos de conteúdo são parte de uma biblioteca, o grupo é removido da página **Adicionar Tipos de Conteúdo** . Se você excluir um ou mais dos tipos de conteúdo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , o grupo **Tipos de Conteúdo do SQL Server Reporting Services** ficará visível na página **Adicionar Tipos de Conteúdo** .  
  
##  <a name="bkmk_enable_content_management_2010"></a> Para habilitar o gerenciamento de tipo de conteúdo para uma única biblioteca de documentos (SharePoint 2010)  
  
1.  Abra a biblioteca para a qual você deseja habilitar vários tipos de conteúdo. Na barra de menus da biblioteca, os seguintes menus serão exibidos: **Novos**, **carregue**, **ações**, e **configurações**. Se **Configurações**não aparecer, você não terá permissão para adicionar um tipo de conteúdo.  
  
2.  Na faixa de opções **Ferramentas de Biblioteca** , clique em **Biblioteca**.  
  
     ![rs_SharePoint2010_LibraryRibbon](media/rs-sharepoint2010-libraryribbon.gif "rs_SharePoint2010_LibraryRibbon")  
  
3.  No grupo da faixa de opções **Configurações** , clique em **Configurações da Biblioteca**.  
  
4.  Em **Configurações Gerais**, clique em **Configurações avançadas**.  
  
5.  Na seção **Tipos de Conteúdo** , selecione **Sim** para permitir o gerenciamento de tipos de conteúdo.  
  
6.  Clique em **OK**.  
  
##  <a name="bkmk_add_single_2010"></a> Para adicionar tipos de conteúdo de servidor de relatório (SharePoint 2010)  
  
1.  Abra a biblioteca para a qual você deseja adicionar tipos de conteúdo do Reporting Services.  
  
2.  Nas guias de faixa de opções **Ferramentas de Biblioteca** , clique na **guia de Biblioteca**.  
  
3.  No grupo da faixa de opções **Configurações** , clique em **Configurações da Biblioteca**.  
  
4.  Em **Tipos de Conteúdo**, clique em **Adicionar a partir de tipos de conteúdo de site existentes**.  
  
5.  Na seção **Selecionar Tipos de Conteúdo** , em **Selecionar tipos de conteúdo de site de**, clique na seta para selecionar **Tipos de Conteúdo do SQL Server Reporting Services**.  
  
6.  Na lista **Tipos Disponíveis de Conteúdo do Site** , clique em **Construtor de Relatórios**e em **Adicionar** para mover o tipo de conteúdo selecionado para a lista **Tipos de conteúdo a serem adicionados** .  
  
7.  Para adicionar os tipos de conteúdo **Modelo de Relatório** e **Fonte de Dados do Relatório** , repita a etapa anterior.  
  
8.  Quando terminar de adicionar tipos de conteúdo, clique em **OK**.  
  
##  <a name="bkmk_enable_multiple_sites"></a> Para habilitar tipos de conteúdo e gerenciamento de conteúdo para vários sites de BI  
  
1.  Para servidores de relatório do SQL Server Reporting Services 2008 e 2008 R2, você pode habilitar tipos de conteúdo e gerenciamento de conteúdo para vários sites do Business Intelligence Center:  
  
2.  Em Administração Central do SharePoint, clique em **Configurações de Aplicativos Gerais**. Na seção **SQL Server Reporting Services (2008 e 2008 R2)** , clique em **Integração do Reporting Services**.  
  
     ![rs_general_app_settings](media/rs-general-app-settings.gif "rs_general_app_settings")  
  
3.  Clique em **Recurso ativo em todos os conjuntos de sites existentes**.  
  
     ![rs_general_app_settings_old_integrations](media/rs-general-app-settings-old-integrations.gif "rs_general_app_settings_old_integrations")  
  
4.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência à permissão de listas e sites do SharePoint para itens do servidor de relatório](security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [Iniciar o construtor de relatórios &#40;construtor de relatórios&#41;](report-builder/start-report-builder.md)  
  
  
