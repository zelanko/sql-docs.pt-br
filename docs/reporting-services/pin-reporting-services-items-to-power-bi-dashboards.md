---
title: Fixar itens do Reporting Services nos painéis do Power BI | Microsoft Docs
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- pbi
- dashboard
- pin
- powerbi
- power bi integration
ms.assetid: 1d96c3f7-2fd4-40f7-8d1c-14a7f54cdb15
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8bca8f07e927dec72690683e0519e181d79d4f79
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710544"
---
# <a name="pin-reporting-services-items-to-power-bi-dashboards"></a>Fixar itens do Reporting Services nos dashboards do Power BI
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] permite que os usuários fixem itens de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] da barra de ferramentas do visualizador de relatórios em um painel do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] como um novo bloco.   Para fixar, o administrador precisa primeiro integrar o servidor de relatório ao Azure Active Directory e ao [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
 ![rs_powerbi_icon](../reporting-services/media/ssrs-powerbi-icon.png "rs_powerbi_icon")  
  
 [!INCLUDE[applies](../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nativo
  
##  <a name="bkmk_requirements_to_pin"></a> Requisitos para fixação  
  
-   O servidor de relatório é configurado para integração do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] . Para obter mais informações, consulte [Integração do servidor de relatório do Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md). Se o servidor de relatório não tiver sido configurado, você não verá o botão **Fixar no painel do Power BI** na barra de ferramentas.  
  
     ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
-   Fixe por meio do visualizador de relatórios do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], por exemplo, `http://myserver/Reports`.  Não é possível fixar do [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)], do designer de relatórios no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], nem de uma url do servidor de relatório.  Por exemplo, `http://myserver/ReportServer`.  
  
-   Seu navegador precisa ser configurado para permitir pop-ups do site do servidor de relatório.  
  
-   Os relatórios precisam ser configurados para credenciais armazenadas, se você quiser que o item fixado seja atualizado.  Quando você fixa um item, uma assinatura do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é criada automaticamente para gerenciar a atualização de dados do item no painel.  Se o relatório não usar credenciais armazenadas, quando a assinatura for executada, você verá uma mensagem de erro semelhante a que se segue na página **Minhas assinaturas** .  
  
        PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credential.
 
    Consulte a seção “Configurar credenciais armazenadas para uma fonte de dados específica do relatório (Modo nativo)” em [Armazenar credenciais em uma fonte de dados do Reporting Services](../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
##  <a name="bkmk_supported_items"></a> Itens que podem ser fixados  
 Os itens de relatório a seguir podem ser fixados em um painel do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  Você não pode fixar itens aninhados dentro de uma região de dados. Por exemplo, não é possível fixar um item aninhado em uma tabela ou lista do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
-   Gráficos  
  
-   Painéis do medidor  
  
-   Mapas  
  
-   Imagens  
  
-   Itens que precisam estar no corpo do relatório.  Você não pode fixar itens que estejam no cabeçalho ou rodapé da página.  
  
-   Você pode fixar itens individuais que estejam dentro de um retângulo de nível superior, mas não pode fixá-los como um único grupo.  
  
##  <a name="bkmk_to_pin"></a> Para fixar um item de relatório  
  
1. Verifique se você está conectado ao [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. No [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], selecione o item de menu **Minhas Configurações** e conecte-se. Confira [Minhas configurações para integração do &#40;portal Web&#41; do Power BI](http://msdn.microsoft.com/85c2fac7-80bf-45b7-8654-764b5f5231f5) para saber mais.

    ![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
2. Navegue até a pasta [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] que contém o relatório e exiba-o.  
  
3. Ao exibir o relatório, selecione o botão **Fixar no Power BI** na barra de ferramentas.  Você será solicitado a se conectar, caso ainda não o tenha feito.  Se o botão [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] não estiver visível, o servidor de relatório não foi integrado ao [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Para obter mais informações, consulte [Integração do servidor de relatório do Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
    ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
4. Clique no item de relatório que você quer fixar no [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Você só pode fixar um item de cada vez.  O visualizador de relatórios apresenta uma exibição sombreada do seu relatório, e os itens de relatório que podem ser fixados são realçados, enquanto os itens que não podem ser fixados aparecerão com um sombreado escuro.  
  
    **(1)** selecione o grupo que contém o painel que você quer fixar, **(2)** selecione o painel no qual você quer fixar o item e **(3)** selecione a frequência com que você quer que o bloco seja atualizado no dashboard.   ![observação](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "note") A atualização é gerenciada pelas assinaturas do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e, depois que o item é fixado, você pode editar a assinatura e configurar outro agendamento de atualização.  
  
    ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png)  
  
5. Selecione **Fixar**  
  
    Na caixa de diálogo **Fixação Bem-Sucedida** , você pode selecionar o link **Ver no Power BI** para navegar até o painel e ver o item que você acabou de fixar.  
  
6. Selecione **Fechar** para retornar o relatório para a exibição normal.  
  
##  <a name="bkmk_in_the_dashboard"></a> No painel

Depois que o item de relatório estiver fixado no painel, o bloco se parecerá com outros blocos do painel e não haverá indicação visível de que o bloco é do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. A lista a seguir resume como as propriedades de bloco são populadas no item de relatório.  
  
No painel do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] , o item de relatório fixado se comporta como outros blocos:

**(1)** Você pode fixar o bloco em outros painéis.

**(2)** Em **Detalhes do Bloco** , você observará que o título do relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é usado para o título padrão do bloco.

**(3)** O subtítulo do bloco é baseado na data e hora em que o bloco foi fixado ou nos dados que foram atualizados pela última vez no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. O agendamento da atualização é gerenciado pela assinatura do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que foi criada automaticamente quando você fixou o item de relatório.

**(4)** Se você selecionar o próprio bloco, o [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] usará o **(3) link personalizado** para navegar até a página do [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] do servidor de relatório registrado. O link foi definido quando o item foi fixado do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Se você não tiver conectividade de Internet com o servidor de relatório, um erro será exibido no navegador.  

![ssrs_pinned_tile_details](../reporting-services/media/ssrs-pinned-tile-details.png "ssrs_pinned_tile_details")  
  
##  <a name="bkmk-troubleshoot"></a> Solucionar problemas  
  
-   **O botão [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] não está visível na barra de ferramentas do visualizador de relatórios:** isso indica que o servidor de relatório não foi integrado ao [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Para obter mais informações, consulte [Integração do servidor de relatório do Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
- **Não é possível fixar**: ao tentar fixar um item, você verá a seguinte mensagem de erro: Consulte a seção [Itens que podem ser fixados](#bkmk_supported_items).  
  
      Cannot Pin: There are no report items on this page that you can pin to [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
-   **Itens fixados mostram dados obsoletos** em um painel do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] e ele foi atualizado por um período.  O token de credenciais do usuário expirou e você precisa se conectar novamente.  O registro da credencial do usuário no Azure e no [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] é válido por 90 dias. No[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], clique em **Minhas Configurações**. Para obter mais informações, consulte [Minhas Configurações para integração do Power BI &#40;portal da Web&#41;](http://msdn.microsoft.com/85c2fac7-80bf-45b7-8654-764b5f5231f5).  
  
-   **Itens fixados mostram dados obsoletos** em um painel do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] e ele não foi atualizado nem mesmo uma vez.  O problema é que o relatório não foi configurado para usar credenciais armazenadas. Um relatório deve usar credenciais armazenadas porque a ação de fixar um item de relatório cria uma assinatura do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para gerenciar o agendamento de atualização dos blocos. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] exigem credenciais armazenadas. Ao analisar a página **Minhas Assinaturas** , você verá uma mensagem de erro semelhante à seguinte:  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified. (rsInvalidDataSourceCredentialSetting)
  
-   **As credenciais do Power BI expiraram:**  você tenta fixar um item e vê a mensagem de erro a seguir. No [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], clique em **Minhas Configurações** e, na página Minhas Configurações, clique em **Entrar**. Confira [Minhas configurações para integração do &#40;portal Web&#41; do Power BI](http://msdn.microsoft.com/85c2fac7-80bf-45b7-8654-764b5f5231f5) para saber mais.  
  
        Cannot Pin : Unexpected Server Error: Missing, invalid or expired Power BI credentials.  
  
-   **Não é possível fixar**: se você tentar fixar um item em um painel que já está em um estado somente leitura, você verá uma mensagem de erro semelhante à seguinte:  
  
        Server Error : The item 'Dashboard deleted 015cf022-8e2f-462e-88e5-75ab0a04c4d0' cannot be found. (rsItemNotFound)  
  
##  <a name="bkmk_subscription_management"></a> Gerenciamento de assinatura  
 Além dos problemas relacionados à assinatura descritos na seção de solução de problemas, as informações a seguir ajudarão você a manter as assinaturas relacionadas ao [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .
  
-   **Nome do item alterado:** se um item de relatório fixado for renomeado ou excluído, o bloco do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] não será mais atualizado e você verá uma mensagem de erro semelhante a que se segue.  Se você renomear o item de volta para o nome original, a assinatura começará a funcionar novamente e o bloco será atualizado no agendamento das assinaturas.  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image1, error: Error: Report item 'Image1' cannot be found.  
  
     Você também pode editar as propriedades de assinatura e alterar o **Nome Visual do Relatório** para o nome do item de relatório apropriado. ![alterar o visual usado para a atualização do Power BI](../reporting-services/media/ssrs-powerbi-subscription-visual.png "alterar o visual usado para a atualização do Power BI")  
  
-   **Excluir um bloco**. Se você excluir um bloco no [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)], a assinatura associada não será excluída no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e, na página **Minhas assinaturas**, um erro semelhante ao que se segue será exibido. É possível excluir a assinatura.  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The item 'Tile deleted af7131d9-5eaf-480f-ba45-943a07d19c9f' cannot be found.  

## <a name="video"></a>Vídeo

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="see-also"></a>Consulte Também  
 [Integração do servidor de relatório do Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [Minhas configurações para integração do &#40;portal Web&#41; do Power BI](http://msdn.microsoft.com/85c2fac7-80bf-45b7-8654-764b5f5231f5)  
 [Painéis no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

