---
title: Referência de parâmetro de acesso à URL | Microsoft Docs
description: Use os parâmetros deste artigo como parte de uma URL para configurar a aparência de seus relatórios do Reporting Services.
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ac67de4831d1785f17029bc6c68fa6f7d8aeb16
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2020
ms.locfileid: "77147379"
---
# <a name="url-access-parameter-reference"></a>Referência de parâmetro de acesso à URL

  Use os parâmetros a seguir como parte de uma URL para configurar a aparência de seus relatórios do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Os parâmetros mais comuns estão listados nesta seção. Os parâmetros não diferenciam maiúsculas de minúsculas e começam com o prefixo de parâmetro *rs:* quando direcionados ao servidor de relatório e com *rc:* quando direcionados a um Visualizador de HTML. Você também pode especificar parâmetros que são específicos de dispositivos ou extensões de renderização. Para obter mais informações sobre parâmetros específicos do dispositivo, confira [Especificar as configurações de informações do dispositivo em uma URL](../reporting-services/specify-device-information-settings-in-a-url.md).
  
> [!IMPORTANT]  
>  Para um servidor de relatório no modo do SharePoint, é importante que a URL inclua a sintaxe do proxy `_vti_bin` para encaminhar a solicitação por meio do SharePoint e do proxy HTTP do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. O proxy adiciona o contexto à solicitação HTTP que é necessário para garantir a execução adequada do relatório para servidores de relatório no modo do SharePoint. Para obter exemplos, confira [Acessar itens do servidor de relatório usando o acesso à URL](../reporting-services/access-report-server-items-using-url-access.md).
> 
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  

##  <a name="bkmk_htmlviewer"></a> Comandos do Visualizador de HTML (rc:)
 - Os comandos do Visualizador de HTML são usados para se destinar ao Visualizador de HTML e são prefixados com *rc:* :
  
-   **Toolbar**: Mostra ou oculta a barra de ferramentas. Se o valor desse parâmetro for **false**, todas as demais opções serão ignoradas. Se você omitir esse parâmetro, a barra de ferramentas será exibida automaticamente para renderizar formatos que dão suporte a ele. O padrão desse parâmetro é **true**.
  
    > [!IMPORTANT]  
    >  *rc:Toolbar*=**false** não funciona em cadeias de caracteres de acesso à URL que usam um endereço IP, em vez de um nome de domínio, para se destinar a um relatório hospedado em um site do SharePoint.
  
-   **Parâmetros**: Mostra ou oculta a área de parâmetros da barra de ferramentas. Se você definir esse parâmetro como **true**, a área de parâmetros da barra de ferramentas será exibida. Se você definir esse parâmetro como **false**, a área de parâmetros não será exibida e não poderá ser vista pelo usuário. Se você definir esse parâmetro com um valor igual a **Collapsed**, a área de parâmetros não será exibida, mas poderá ser ativada/desativada pelo usuário. O valor padrão desse parâmetro é **true**.  
  
     Por exemplo, no modo nativo:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Parameters=Collapsed  
    ```  
  
     Por exemplo, no modo do SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Parameters=Collapsed  
    ```  
  
-   **Zoom**: Define o valor de zoom do relatório como uma porcentagem de número inteiro ou uma constante de cadeia de caracteres. Os valores de cadeia de caracteres padrão incluem **Page Width** e **Whole Page**. Esse parâmetro é ignorado pelas versões do Internet Explorer anteriores ao Internet Explorer 5.0 e todos os navegadores que não são da[!INCLUDE[msCoName](../includes/msconame-md.md)] . O valor padrão desse parâmetro é **100**.
  
     Por exemplo, no modo nativo:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Zoom=Page Width  
    ```  
  
     Por exemplo, no modo do SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Zoom=Page Width  
    ```  
  
-   **Section**: Define a página do relatório a ser exibida. Qualquer valor maior que o número de páginas do relatório exibe a última página. Qualquer valor inferior a **0** exibe a página 1 do relatório. O valor padrão desse parâmetro é **1**.
  
     Por exemplo, no modo nativo, para exibir a página 2 do relatório:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Section=2  
    ```  
  
     Por exemplo, no modo do SharePoint, para exibir a página 2 do relatório:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Section=2  
    ```  
  
-   **FindString**: Pesquise um relatório por um conjunto específico de texto.
  
     Por exemplo, no modo nativo:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:FindString=Mountain-400  
    ```  
  
     Por exemplo, no modo do SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:FindString=Mountain-400  
    ```  
  
-   **StartFind**: Especifica a última seção a ser pesquisada. O valor padrão desse parâmetro é a última página do relatório.  
  
     Para obter um exemplo no modo nativo que pesquisa a primeira ocorrência do texto "Mountain-400" no relatório de exemplo do Catálogo de Produtos começando na página 1 e terminando na página 5:
  
    ```  
    https://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
    ```  
  
-   **EndFind**: Define o número da última página a ser usada na pesquisa. Por exemplo, um valor **5** indica que a última página a ser pesquisada é a página 5 do relatório. O valor padrão é o número da página atual. Use esse parâmetro junto com o parâmetro *StartFind* . Confira o exemplo anterior.
  
-   **FallbackPage**: Define o número da página a ser exibido em caso de falha em uma pesquisa ou em uma seleção do mapa do documento. O valor padrão é o número da página atual.
  
-   **GetImage**: Obtém um ícone específico para a interface de usuário do Visualizador de HTML.
  
-   **Icon**: Obtém o ícone de uma extensão de renderização específica.
  
-   **Stylesheet**: Especifica uma folha de estilos a ser se aplicada ao Visualizador de HTML.
  
-   **Configuração de Informações do Dispositivo**: especifica uma configuração de informações do dispositivo no formato `rc:tag=value`, em que *tag* é o nome de uma configuração de informações do dispositivo específica da extensão de renderização atualmente usada. (Confira a descrição do parâmetro *Format*.) Por exemplo, você pode usar a configuração de informações do dispositivo *OutputFormat* para que a extensão de renderização de IMAGE renderize o relatório em uma imagem JPEG usando os seguintes parâmetros na cadeia de caracteres de acesso à URL: `...&rs:Format=IMAGE&rc:OutputFormat=JPEG`. Para obter mais informações sobre todas as configurações de informações do dispositivo específicas da extensão, confira [Configurações de informações do dispositivo para extensões de renderização &#40;Reporting Services&#41;](../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md).
  
##  <a name="bkmk_reportserver"></a> Comandos do servidor de relatório (rs:)
 Os comandos do servidor de relatório são prefixados com *rs:* e são usados para se destinar ao servidor de relatório:
  
-   **Comando**: Executa uma ação em um item do catálogo, dependendo do tipo do item. O valor padrão é determinado pelo tipo do item do catálogo referenciado na cadeia de caracteres de acesso à URL. Os valores válidos são:
  
    -   **ListChildren** e **GetChildren**: exibem o conteúdo de uma pasta. Os itens dessa pasta são exibidos em uma página da navegação de item genérica.
  
         Por exemplo, no modo nativo:
  
        ```  
        https://myrshost/reportserver?/Sales&rs:Command=GetChildren  
        ```  
  
         Por exemplo, uma instância nomeada no modo nativo:
  
        ```  
        https://myssrshost/Reportserver_THESQLINSTANCE?/reportfolder&rs:Command=listChildren  
        ```  
  
         Por exemplo, no modo do SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rs:Command=GetChildren  
        ```  
  
    -   **Renderizar**: o relatório é renderizado no navegador para que você possa vê-lo.
  
         Por exemplo, no modo nativo:
  
        ```  
        https://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
         Por exemplo, no modo do SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
    -   **GetSharedDatasetDefinition**: exibe a definição de XML associada a um conjunto de dados compartilhado. As propriedades do conjunto de dados compartilhado, inclusive a consulta, os parâmetros do conjunto de dados, os valores padrão, os filtros de conjunto de dados e as opções de dados, como ordenação e diferenciação entre maiúsculas e minúsculas, são salvas na definição. É necessário ter a permissão **Ler Definição de Relatório** em um conjunto de dados compartilhado para usar esse valor.
  
         Por exemplo, no modo nativo:
  
        ```  
        https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
        ```  
  
    -   **GetDataSourceContents**: exibe as propriedades de determinada fonte de dados compartilhada como XML. Se houver suporte para XML no navegador e se você for um usuário autenticado com a permissão **Ler Conteúdo** na fonte de dados, a definição de fonte de dados será exibida.
  
         Por exemplo, no modo nativo:
  
        ```  
        https://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
         Por exemplo, no modo do SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
    -   **GetResourceContents**: renderiza um recurso e o exibe em uma página HTML se o recurso é compatível com o navegador. Caso contrário, você deverá abrir ou salvar o arquivo ou o recurso em disco.  
  
         Por exemplo, no modo nativo:
  
        ```  
        https://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents  
        ```  
  
         Por exemplo, no modo do SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents  
        ```  
  
    -   **GetComponentDefinition**: exibe a definição de XML associada a um item de relatório publicado. É necessário ter a permissão **Ler Conteúdo** em um item de relatório publicado para usar esse valor.
  
-   **Formatar**: Especifica o formato no qual um relatório deve ser renderizado e exibido. Os valores comuns incluem:
  
    -   **HTML5**  
  
    -   **PPTX**  
  
    -   **ATOM**  
  
    -   **HTML4.0**  
  
    -   **MHTML**  
  
    -   **IMAGE**  
  
    -   **EXCEL** (para .xls)
    
    -   **EXCELOPENXML** (para .xlsx)
  
    -   **WORD** (para .doc)
    
    -   **WORDOPENXML** (para .docx)
  
    -   **CSV**  
  
    -   **PDF**  
  
    -   **XML**  
  
     O valor padrão é **HTML5**. Para obter mais informações, confira [Exportar um relatório usando o acesso à URL](../reporting-services/export-a-report-using-url-access.md).
  
     Para obter uma lista completa, consulte a seção da extensão **\<Render>** do arquivo rsreportserver.config do servidor de relatório. Para obter informações sobre o local em que o arquivo pode ser encontrado, confira [Arquivo de configuração RsReportServer.config](../reporting-services/report-server/rsreportserver-config-configuration-file.md).
  
     Por exemplo, para obter uma cópia em PDF de um relatório diretamente de um servidor de relatório de modo nativo:
  
    ```  
    https://myrshost/ReportServer?/myreport&rs:Format=PDF  
    ```  
  
     Por exemplo, para obter uma cópia em PDF de um relatório diretamente de um servidor de relatório no modo do SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
    ```  
  
-   **ParameterLanguage**: fornece um idioma para os parâmetros transmitidos em uma URL que não depende do idioma do navegador. O valor padrão é o idioma do pesquisador. O valor pode ser um valor de cultura, como **en-us** ou **de-de.**
  
     Por exemplo, no modo nativo, para substituir o idioma do navegador e especificar um valor de cultura de-DE:
  
    ```  
    https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
    ```  
  
-   **Instantâneo**: Renderiza um relatório com base em um instantâneo de histórico de relatório. Para obter mais informações, confira [Renderizar um instantâneo de histórico de relatórios usando o acesso à URL](../reporting-services/render-a-report-history-snapshot-using-url-access.md).
  
     Por exemplo, no modo nativo, recupere um instantâneo de histórico de relatórios datado de 2003-04-07 com um carimbo de data/hora 13:40:02:
  
    ```  
    https://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
    ```  
  
-   **PersistStreams**: Renderiza um relatório em um único fluxo persistido. Esse parâmetro é usado pelo renderizador de imagem para transmitir uma parte de cada vez do relatório renderizado. depois de usar esse parâmetro em uma cadeia de caracteres de acesso à URL, use a mesma cadeia de caracteres de acesso à URL com o parâmetro *GetNextStream* em vez do parâmetro *PersistStreams* para obter a próxima parte do fluxo persistido. Esse comando de URL acaba retornando um fluxo de 0 byte para indicar o fim do fluxo persistente. O valor padrão é **false**.
  
-   **GetNextStream**: obtém a próxima parte de dados em um fluxo persistente acessado com o parâmetro *PersistStreams*. Para obter mais informações, consulte a descrição de *PersistStreams*. O valor padrão é **false**.
  
-   **SessionID**: Especifica uma sessão de relatório ativa estabelecida entre o aplicativo cliente e o servidor de relatório. O valor desse parâmetro é definido como o identificador de sessão.
  
     Você pode especificar a ID da sessão como um cookie ou como parte da URL. Quando o servidor de relatório tiver sido configurado para não usar cookies de sessão, a primeira solicitação sem uma ID de sessão especificada resultará no redirecionamento com uma ID de sessão. Para obter mais informações sobre as sessões do servidor de relatório, confira [Como identificar o estado de execução](../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md).
  
-   **ClearSession**: Um valor **true** direciona o servidor de relatório a remover um relatório da sessão de relatório. Todas as instâncias de relatório associadas a um usuário autenticado são removidas da sessão de relatório. (Uma instância de relatório será definida já que o mesmo relatório é executado várias vezes com valores de parâmetro de relatório diferentes.) O valor padrão é **false**.
  
-   **ResetSession**: Um valor **true** direciona o servidor de relatório a redefinir a sessão de relatório removendo a associação da sessão de relatório a todos os instantâneos de relatório. O valor padrão é **false**.
  
-   **ShowHideToggle**: Alterna o estado de mostrar e ocultar de uma seção do relatório. Especifique um número inteiro positivo para representar a seção a ser alternada.
  
##  <a name="bkmk_webpart"></a> Comandos da web part do Visualizador de Relatórios (rv:)
 Os nomes de parâmetros de relatório reservados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a seguir são usados para se destinar à web part do Visualizador de Relatórios integrada ao SharePoint. Esses nomes de parâmetro são prefixados com *rv:* . A web part do Visualizador de Relatórios também aceita o parâmetro *rs:ParameterLanguage*.
  
-   **Toolbar**: Controla a exibição da barra de ferramentas para a web part do Visualizador de Relatórios. O valor padrão é **Completo**. Os valores podem ser:
  
    -   **Full**: exibe a barra de ferramentas completa.
  
    -   **Navegação**: exibe apenas a paginação na barra de ferramentas.
  
    -   **Nenhum**: não exibe a barra de ferramentas.
  
     Por exemplo, no modo do SharePoint, para exibir apenas a paginação na barra de ferramentas:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation  
    ```  
  
-   **HeaderArea**: Controla a exibição do cabeçalho para a web part do Visualizador de Relatórios. O valor padrão é **Completo**. Os valores podem ser:
  
    -   **Full**: exibe o cabeçalho completo.
  
    -   **BreadCrumbsOnly**: exibe apenas a navegação estrutural no cabeçalho para informar ao usuário a localização dele no aplicativo.
  
    -   **Nenhum**: não exibe o cabeçalho.
  
     Por exemplo, no modo do SharePoint, para exibir apenas a navegação estrutural no cabeçalho:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly  
    ```  
  
-   **DocMapAreaWidth**: Controla a largura de exibição, em pixels, da área de parâmetro na web part do Visualizador de Relatórios. O valor padrão é o mesmo do padrão da web part do Visualizador de Relatórios. O valor deve ser um inteiro não negativo.
  
-   **AsyncRender**: Controla se um relatório é renderizado de forma assíncrona. O valor padrão é **true**, que especifica que um relatório deve ser renderizado de forma assíncrona. O valor deve ser um booliano **true** ou **false**.
  
-   **ParamMode**: Controla como a área de aviso de parâmetros da web part do Visualizador de Relatórios é mostrada na exibição de página inteira. O valor padrão é **Completo**. Os valores válidos são:
  
    -   **Full**: exibe a área de aviso de parâmetros.
  
    -   **Collapsed**: recolhe a área de aviso de parâmetros.
  
    -   **Hidden**: oculta a área de aviso de parâmetros.
  
     Por exemplo, no modo do SharePoint, para recolher a área de aviso de parâmetros:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed  
    ```  
  
-   **DocMapMode**: Controla como a área do mapa do documento da web part do Visualizador de Relatórios é mostrada na exibição de página inteira. O valor padrão é **Completo**. Os valores válidos são:
  
    -   **Full**: exibe a área de mapa do documento.
  
    -   **Collapsed**: recolhe a área de mapa do documento.
  
    -   **Hidden**: oculta a área de mapa do documento.
  
-   **DockToolBar**: Controla se a barra de ferramentas da web part do Visualizador de Relatórios está encaixada na parte superior ou na parte inferior. Os valores válidos são **Top** e **Bottom**. O valor padrão é **Top**.
  
     Por exemplo, no modo do SharePoint, para encaixar a barra de ferramentas na parte inferior:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom  
    ```  
  
-   **ToolBarItemsDisplayMode**: Controlar quais itens da barra de ferramentas são exibidos. Esse é um valor de enumeração de bit a bit. Para incluir um item de barra de ferramentas, adicione o valor do item ao valor total. Por exemplo, para nenhum menu de **Ações**, use *rv:ToolBarItemsDisplayMode=63* (ou 0x3F), que é 1 + 2 + 4 + 8 + 16 + 32. Para somente itens de menu **Ações**, use *rv:ToolBarItemsDisplayMode=960* (ou 0x3C0). O valor padrão é **-1**, que inclui todos os itens da barra de ferramentas. Os valores válidos são:
  
    -   **1 (0x1)** : o botão **Voltar**  
  
    -   **2 (0x2)** : os controles de pesquisa de texto  
  
    -   **4 (0x4)** : os controles de navegação de página  
  
    -   **8 (0x8)** : o botão **Atualizar**  
  
    -   **16 (0x10)** : a caixa de listagem **Zoom**  
  
    -   **32 (0x20)** : o botão **Feed Atom**  
  
    -   **64 (0x40)** : a opção de menu **Imprimir** em **Ações**  
  
    -   **128 (0x80)** : o submenu **Exportar** em **Ações**  
  
    -   **256 (0x100)** : a opção de menu **Abrir com o Construtor de Relatórios** em **Ações**  
  
    -   **512 (0x200)** : a opção de menu **Assinar** em **Ações**  
  
    -   **1024 (0x400)** : a opção de menu **Novo Alerta de Dados** em **Ações**  
  
     Por exemplo, no modo do SharePoint, para exibir apenas o botão **Voltar**, os controles de pesquisa de texto, os controles de navegação de página e o botão **Atualizar**:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15  
    ```  
  
## <a name="see-also"></a>Confira também
 - [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)
 - [Exportar um relatório usando o acesso à URL](../reporting-services/export-a-report-using-url-access.md)
  
  
