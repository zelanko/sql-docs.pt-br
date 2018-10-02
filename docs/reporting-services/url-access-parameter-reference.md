---
title: Referência de parâmetro de acesso à URL | Microsoft Docs
ms.date: 09/09/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1ec74bab3523b4e77c1b1c0c9355353c48490140
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817535"
---
# <a name="url-access-parameter-reference"></a>Referência de parâmetro de acesso de URL
  Você pode usar os parâmetros a seguir como parte de uma URL para configurar a aparência de seus relatórios do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Os parâmetros mais comuns estão listados nesta seção. Os parâmetros não diferenciam maiúsculas de minúsculas e começam com o prefixo de parâmetro *rs:* quando direcionados ao servidor de relatório e com *rc:* quando direcionados a um Visualizador de HTML. Você também pode especificar parâmetros que são específicos de dispositivos ou extensões de renderização. Para obter mais informações sobre parâmetros específicos do dispositivo, consulte [Especificar as configurações de informações sobre o dispositivo em uma URL](../reporting-services/specify-device-information-settings-in-a-url.md).  
  
> [!IMPORTANT]  
>  Para um servidor de relatório no modo do SharePoint, é importante que a URL inclua a sintaxe do proxy `_vti_bin` para encaminhar a solicitação por meio do SharePoint e do proxy HTTP [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . O proxy adiciona contexto à solicitação HTTP que é necessário para garantir a execução adequada do relatório para servidores de relatório no modo do SharePoint. Para obter exemplos, consulte [Acessar itens do Servidor de Relatório usando o acesso à URL](../reporting-services/access-report-server-items-using-url-access.md).  
>   
>  Para obter informações sobre como incluir parâmetros de relatório em uma URL, além de exemplos, consulte [Passar um parâmetro de relatório em uma URL](../reporting-services/pass-a-report-parameter-within-a-url.md).  
  
##  <a name="bkmk_top"></a> Neste tópico  
  
-   [Comandos do Visualizador HTML (rc:)](#bkmk_htmlviewer)  
  
-   [Comandos do servidor de relatório (rs:)](#bkmk_reportserver)  
  
-   [Comandos da Web Part do Visualizador de Relatórios (rv:)](#bkmk_webpart)  
  
##  <a name="bkmk_htmlviewer"></a> Comandos do Visualizador HTML (rc:)  
 Os comandos do Visualizador de HTML são usados para destinar-se ao Visualizador de HTML (por exemplo, do Gerenciador de Relatórios) e são prefixados com *rc:*:  
  
-   *Toolbar* :  
                  Mostra ou oculta a barra de ferramentas. Se o valor desse parâmetro for **false**, todas as demais opções serão ignoradas. Se você omitir esse parâmetro, a barra de ferramentas será exibida automaticamente para renderizar formatos que dão suporte a ele. O padrão desse parâmetro é **true**.  
  
    > [!IMPORTANT]  
    >  *rc:Toolbar*=**false** não funciona para cadeias de caracteres de acesso à URL que usam um endereço IP, em vez de um nome de domínio, para se destinar a um relatório hospedado em um site do SharePoint.  
  
-   *Parameters* : mostra ou oculta a área de parâmetros da barra de ferramentas. Se você definir esse parâmetro como **true**, a área de parâmetros da barra de ferramentas será exibida. Se você definir esse parâmetro como **false**, a área de parâmetros não será exibida e não poderá ser exibida pelo usuário. Se você definir esse parâmetro com um valor **Collapsed**, a área de parâmetros não será exibida, mas poderá ser ativada/desativada pelo usuário final. O valor padrão desse parâmetro é **true**.  
  
     Para obter um exemplo no modo **Nativo** :  
  
    ```  
    http://myrshost/reportserver?/Sales&rc:Parameters=Collapsed  
    ```  
  
     Para obter um exemplo no modo do **SharePoint** :  
  
    ```  
    http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Parameters=Collapsed  
    ```  
  
-   *Zoom* : define o valor de zoom do relatório como um percentual de número inteiro ou uma constante de cadeia de caracteres. Os valores de cadeia de caracteres padrão incluem **Page Width** e **Whole Page**. Esse parâmetro é ignorado pelas versões do Internet Explorer anteriores ao Internet Explorer 5.0 e todos os navegadores que não são da[!INCLUDE[msCoName](../includes/msconame-md.md)] . O valor padrão desse parâmetro é **100**.  
  
     Por exemplo, no modo **Nativo** :  
  
    ```  
    http://myrshost/reportserver?/Sales&rc:Zoom=Page Width  
    ```  
  
     Por exemplo, no modo do **SharePoint** .  
  
    ```  
    http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Zoom=Page Width  
    ```  
  
-   *Section* : define a página do relatório a ser exibida. Qualquer valor maior que o número de páginas do relatório exibe a última página. Qualquer valor menor que **0** exibe a página 1 do relatório. O valor padrão desse parâmetro é **1**.  
  
     Por exemplo, no modo **Nativo** , para exibir a página 2 do relatório:  
  
    ```  
    http://myrshost/reportserver?/Sales&rc:Section=2  
    ```  
  
     Por exemplo, no modo do **SharePoint** , para exibir a página 2 do relatório:  
  
    ```  
    http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Section=2  
    ```  
  
-   *FindString*: pesquise um conjunto específico de texto em um relatório.  
  
     Para obter um exemplo no modo **Nativo** .  
  
    ```  
    http://myrshost/reportserver?/Sales&rc:FindString=Mountain-400  
    ```  
  
     Por exemplo, no modo do **SharePoint** .  
  
    ```  
    http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:FindString=Mountain-400  
    ```  
  
-   *StartFind* : especifica a última seção a ser pesquisada. O valor padrão desse parâmetro é a última página do relatório.  
  
     Para obter um exemplo no modo **Nativo** que pesquisa a primeira ocorrência do texto “Mountain-400” no relatório de exemplo Catálogo de Produtos começando pela primeira página e terminando na página cinco.  
  
    ```  
    http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
    ```  
  
-   *EndFind* : define o número da última página a ser usada na pesquisa. Por exemplo, um valor **5** indica que a última página a ser pesquisada é a página 5 do relatório. O valor padrão é o número da página atual. Use esse parâmetro junto com o parâmetro *StartFind* . Consulte o exemplo acima.  
  
-   *FallbackPage* : define o número da página a ser exibido em caso de falha em uma pesquisa ou em uma seleção do mapa do documento. O valor padrão é o número da página atual.  
  
-   *GetImage* : obtém um ícone específico para a interface do usuário do Visualizador de HTML.  
  
-   *Icon* : obtém o ícone de uma extensão de renderização específica.  
  
-   *Stylesheet*: especifica uma folha de estilos a ser aplicada ao Visualizador de HTML.  
  
-   Configuração de Informações sobre o Dispositivo: especifica uma configuração de informações de dispositivo no formulário de `rc:tag=value`, em que *tag* é o nome de uma configuração de informações de dispositivo específicas da extensão de renderização usada atualmente (consulte a descrição do parâmetro *Format* ). Por exemplo, você pode usar a configuração de informações sobre o dispositivo *OutputFormat* para que a extensão de renderização de IMAGE renderize o relatório em uma imagem JPEG usando os seguintes parâmetros na cadeia de caracteres de acesso à URL: `…&rs:Format=IMAGE&rc:OutputFormat=JPEG`. Para obter mais informações sobre todas as configurações de informações sobre o dispositivo específicas da extensão, consulte [Configurações de informações sobre o dispositivo para extensões de renderização &#40;Reporting Services&#41;](../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md).  
  
##  <a name="bkmk_reportserver"></a> Comandos do servidor de relatório (rs:)  
 Os comandos do servidor de relatório são prefixados com *rs:* e são usados para se destinar ao servidor de relatório:  
  
-   *Command*:  
                  Executa uma ação em um item do catálogo, dependendo do tipo do item. O valor padrão é determinado pelo tipo do item do catálogo referenciado na cadeia de caracteres de acesso à URL. Os valores válidos são:  
  
    -   **ListChildren** e **GetChildren** Exibem o conteúdo de uma pasta. Os itens dessa pasta são exibidos em uma página da navegação de item genérica.  
  
         Por exemplo, no modo **Nativo** .  
  
        ```  
        http://myrshost/reportserver?/Sales&rs:Command=GetChildren  
        ```  
  
         Por exemplo, uma instância nomeada no modo **Nativo** .  
  
        ```  
        http://myssrshost/Reportserver_THESQLINSTANCE?/reportfolder&rs:Command=listChildren  
        ```  
  
         Por exemplo, no modo do **SharePoint** .  
  
        ```  
        http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren  
        ```  
  
    -   **Render** O relatório é renderizado no navegador para que você possa exibi-lo.  
  
         Por exemplo, no modo **Nativo** :  
  
        ```  
        http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
         Por exemplo, no modo do **SharePoint** .  
  
        ```  
        http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
    -   **GetSharedDatasetDefinition** Exibe a definição XML associada a um conjunto de dados compartilhado. As propriedades do conjunto de dados compartilhado, inclusive a consulta, os parâmetros do conjunto de dados, os valores padrão, os filtros de conjunto de dados e as opções de dados, como agrupamento e diferenciação entre maiúsculas e minúsculas, são salvas na definição. É necessário ter a permissão **Ler Definição de Relatório** em um conjunto de dados compartilhado para usar esse valor.  
  
         Por exemplo, no modo **Nativo** .  
  
        ```  
        http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
        ```  
  
    -   **GetDataSourceContents** Exibe as propriedades de determinada fonte de dados compartilhada como XML. Se houver suporte para XML em seu navegador e se você for um usuário autenticado com a permissão **Ler Conteúdo** na fonte de dados, a definição de fonte de dados será exibida.  
  
         Por exemplo, no modo **Nativo** .  
  
        ```  
        http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
         Por exemplo, no modo do **SharePoint** .  
  
        ```  
        http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
    -   **GetResourceContents** Renderizará um recurso e o exibirá em uma página HTML se o recurso for compatível com o navegador. Caso contrário, você será solicitado a abrir ou salvar o arquivo ou recurso em disco.  
  
         Por exemplo, no modo **Nativo** .  
  
        ```  
        http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents  
        ```  
  
         Por exemplo, no modo do **SharePoint** .  
  
        ```  
        http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents  
        ```  
  
    -   **GetComponentDefinition** Exibe a definição XML associada a um item de relatório publicado. É necessário ter a permissão **Ler Conteúdo** em um item de relatório publicado para usar esse valor.  
  
-   *Formato* :  
                  Especifica o formato no qual um relatório deve ser renderizado e exibido. Os valores comuns incluem:  
  
    -   **HTML5**  
  
    -   **PPTX**  
  
    -   **ATOM**  
  
    -   **HTML4.0**  
  
    -   **MHTML**  
  
    -   **IMAGE**  
  
    -   **EXCEL**  
  
    -   **WORD**  
  
    -   **CSV**  
  
    -   **PDF**  
  
    -   **XML**  
  
     O valor padrão é **HTML5**. Para saber mais, confira [Export a Report Using URL Access](../reporting-services/export-a-report-using-url-access.md).  
  
     Para obter uma lista completa, consulte a seção da extensão **\<Render>** do arquivo rsreportserver.config do servidor de relatório.  Para obter informações sobre onde encontrar o arquivo, consulte [Arquivo de configuração RsReportServer.config](../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
     Por exemplo, para obter uma cópia em PDF de um relatório diretamente de um servidor de relatório no modo **Nativo** :  
  
    ```  
    http://myrshost/ReportServer?/myreport&rs:Format=PDF  
    ```  
  
     Por exemplo, para obter uma cópia em PDF de um relatório diretamente de um servidor de relatório no modo do **SharePoint** :  
  
    ```  
    http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
    ```  
  
-   *ParameterLanguage*:  
                  Fornece um idioma para parâmetros passados em uma URL que independe do idioma do pesquisador. O valor padrão é o idioma do pesquisador. O valor pode ser um valor de cultura, como **en-us** ou **de-de.**  
  
     Por exemplo, no modo **Nativo** , para substituir o idioma do navegador e especificar um valor de cultura de-DE:  
  
    ```  
    http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
    ```  
  
-   *Snapshot* : renderiza um relatório com base em um instantâneo de histórico de relatório. Para obter mais informações, consulte [Renderizar um instantâneo de histórico de relatório usando o acesso à URL](../reporting-services/render-a-report-history-snapshot-using-url-access.md).  
  
     Por exemplo, no modo **Nativo** , recupere um instantâneo de histórico de relatórios datado de 2003-04-07 com um carimbo de data/hora de 13:40:02:  
  
    ```  
    http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
    ```  
  
-   *PersistStreams*:  
                  Renderiza um relatório em um único fluxo persistido. Esse parâmetro é usado pelo renderizador de imagem para transmitir uma parte de cada vez do relatório renderizado. depois de usar esse parâmetro em uma cadeia de caracteres de acesso à URL, use a mesma cadeia de caracteres de acesso à URL com o parâmetro *GetNextStream* em vez do parâmetro *PersistStreams* para obter a próxima parte do fluxo persistido. Esse comando URL retornará eventualmente um fluxo de 0 byte para indicar o fim do fluxo persistido. O valor padrão é **false**.  
  
-   *GetNextStream*:  
                  obtém a próxima parte de dados em um fluxo persistido acessado com o parâmetro *PersistStreams* . Para obter mais informações, consulte a descrição de *PersistStreams*. O valor padrão é **false**.  
  
-   *SessionID*:  
                  Especifica uma sessão de relatório ativa estabelecida entre o aplicativo cliente e o servidor de relatório. O valor desse parâmetro é definido como o identificador de sessão.  
  
     Você pode especificar a ID da sessão como um cookie ou como parte da URL. Quando o servidor de relatório tiver sido configurado para não usar cookies de sessão, a primeira solicitação sem uma ID de sessão especificada resultará no redirecionamento com uma ID de sessão. Para obter mais informações sobre as sessões do servidor de relatório, consulte [Identificando o estado de execução](../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md).  
  
-   *ClearSession*:  
                  Um valor **true** direciona o servidor de relatório a remover um relatório da sessão de relatório. Todas as instâncias de relatório associadas a um usuário autenticado são removidas da sessão de relatório. (Uma instância de relatório será definida já que o mesmo relatório é executado várias vezes com valores de parâmetro de relatório diferentes). O valor padrão é **false**.  
  
-   *ResetSession*:  
                  Um valor **true** direciona o servidor de relatório a redefinir a sessão de relatório removendo a associação da sessão de relatório a todos os instantâneos de relatório. O valor padrão é **false**.  
  
-   *ShowHideToggle*:  
                  Alterna o estado de mostrar e ocultar de uma seção do relatório. Especifique um número inteiro positivo para representar a seção a ser alternada.  
  
##  <a name="bkmk_webpart"></a> Comandos da Web Part do Visualizador de Relatórios (rv:)  
 O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a seguir descreve os nomes de parâmetros de relatório reservados que são usados para se destinar à Web Part Visualizador de Relatórios integrada ao SharePoint. Esses nomes de parâmetro são prefixados com *rv:*. A Web Part Visualizador de Relatórios também aceita o parâmetro *rs:ParameterLanguage* .  
  
-   *Toolbar*: controla a exibição da barra de ferramentas para a Web Part Visualizador de Relatórios. O valor padrão é **Completo**. Os valores podem ser:  
  
    -   **Full**: exibe a barra de ferramentas completa.  
  
    -   **Navigation**: exibe apenas a paginação na barra de ferramentas.  
  
    -   **None**: não exibe a barra de ferramentas.  
  
     Por exemplo, no modo do **SharePoint** , para exibir apenas a paginação na barra de ferramentas.  
  
    ```  
    http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation  
    ```  
  
-   *HeaderArea*: controla a exibição do cabeçalho da Web Part Visualizador de Relatórios. O valor padrão é **Completo**. Os valores podem ser:  
  
    -   **Full**: exibe o cabeçalho completo.  
  
    -   **BreadCrumbsOnly**: exibe apenas a navegação de trilha no cabeçalho para informar ao usuário sua localização no aplicativo.  
  
    -   **None**: não exibe o cabeçalho.  
  
     Por exemplo, no modo do **SharePoint** , para exibir apenas a navegação de trilha no cabeçalho.  
  
    ```  
    http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly  
    ```  
  
-   *DocMapAreaWidth*: controla a largura de exibição, em pixels, da área de parâmetro na Web Part Visualizador de Relatórios. O valor padrão é o mesmo do padrão da Web Part do Visualizador de Relatórios. O valor deve ser um inteiro não negativo.  
  
-   *AsyncRender*: controla se um relatório é renderizado de forma assíncrona. O valor padrão é **true**, que especifica que um relatório deve ser renderizado de forma assíncrona. O valor deve ser um booliano **true** ou **false**.  
  
-   *ParamMode*: controla como a área de prompt de parâmetros da Web Part Visualizador de Relatórios é exibida na exibição de página inteira. O valor padrão é **Completo**. Os valores válidos são:  
  
    -   **Full**: exibe a área de prompt de parâmetros.  
  
    -   **Collapsed**: recolhe a área de prompt de parâmetros.  
  
    -   **Hidden**: oculta a área de prompt de parâmetros.  
  
     Por exemplo, no modo do **SharePoint** , para recolher a área de prompt de parâmetros.  
  
    ```  
    http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed  
    ```  
  
-   *DocMapMode*: controla como a área do mapa do documento da Web Part Visualizador de Relatórios é exibida na exibição de página inteira. O valor padrão é **Completo**. Os valores válidos são:  
  
    -   **Full**: exibe a área de mapa do documento.  
  
    -   **Collapsed**: recolhe a área de mapa do documento.  
  
    -   **Hidden**: oculta a área de mapa do documento.  
  
-   *DockToolBar*: controla se a barra de ferramentas da Web Part Visualizador de Relatórios é encaixada na parte superior ou na parte inferior. Os valores válidos são **Top** e **Bottom**. O valor padrão é **Top**.  
  
     Por exemplo, no modo do **SharePoint** , para encaixar a barra de ferramentas na parte inferior.  
  
    ```  
    http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom  
    ```  
  
-   *ToolBarItemsDisplayMode*: controla quais itens da barra de ferramentas são exibidos. Esse é um valor de enumeração de bit a bit. Para incluir um item de barra de ferramentas, adicione o valor do item ao valor total. Por exemplo: para nenhum menu Ações, use rv:ToolBarItemsDisplayMode=63 (ou 0x3F) que é 1+2+4+8+16+32; para itens de menu Ações apenas, use rv:ToolBarItemsDisplayMode=960 (ou 0x3C0). O valor padrão é **-1**, que inclui todos os itens da barra de ferramentas. Os valores válidos são:  
  
    -   1 (0x1): o botão **Voltar**  
  
    -   2 (0x2): os controles de pesquisa de texto  
  
    -   4 (0x4): os controles de navegação da página  
  
    -   8 (0x8): o botão **Atualizar**  
  
    -   16 (0x10): a caixa de listagem **Zoom**  
  
    -   32 (0x20): o botão **Feed Atom**  
  
    -   64 (0x40): a opção de menu **Imprimir** em **Ações**  
  
    -   128 (0x80): o submenu **Exportar** em **Ações**  
  
    -   256 (0x100): a opção de menu **Abrir com o Construtor de Relatórios** em **Ações**  
  
    -   512 (0x200): a opção de menu **Assinar** em **Ações**  
  
    -   1024 (0x400): a opção de menu **Novo Alerta de Dados** em **Ações**  
  
     Por exemplo, no modo do **SharePoint** , para exibir somente o botão **Voltar** , os controles de pesquisa de texto, os controles de navegação de página e o botão **Atualizar** .  
  
    ```  
    http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Exportar um relatório com acesso à URL](../reporting-services/export-a-report-using-url-access.md)  
  
  
