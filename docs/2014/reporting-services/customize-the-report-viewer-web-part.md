---
title: Personalizar a Web Part do Visualizador de relatórios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- Report Viewer Web Part [Reporting Services]
ms.assetid: 086d6546-7299-41bc-bca9-083a15a53679
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b9bbccd4abf5636cb777d69b64268ffea6632e65
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947752"
---
# <a name="customize-the-report-viewer-web-part"></a>Personalizar a Web Part do Visualizador de Relatórios
  Você pode usar a Web Part do Visualizador de Relatórios para exibir relatórios executados em um servidor de relatório configurado para integração do SharePoint. Os relatórios que você pode exibir incluem arquivos de definição de relatório (.rdl) e relatórios do Construtor de Relatórios. Os relatórios são abertos na Web Part do Visualizador de Relatórios em uma nova página automaticamente, mas você também pode adicionar uma Web Part do Visualizador de Relatórios a uma página ou site existente se quiser que um determinado relatório sempre esteja visível nessa página.  
  
 Você pode personalizar a Web Part do Visualizador de Relatórios das seguintes formas:  
  
-   Altere a aparência da Web Part definindo propriedades.  
  
-   Escolha quais recursos de relatórios interativos estão disponíveis na barra de ferramentas do relatório.  
  
-   Especifique quais áreas de exibição estão disponíveis. A Web Part do Visualizador de Relatórios tem uma área de exibição de relatório, uma área de Parâmetros e uma área de Credenciais.  
  
 Você não pode ampliar a Web Part do Visualizador de Relatórios para oferecer suporte a diferentes tipos de arquivos e não pode substituir a barra de ferramentas do relatório por uma barra de ferramentas personalizada nem adicionar nova funcionalidade à barra de ferramentas existente. Se você precisar de personalização de recursos padrão, deverá criar uma Web Part personalizada.  
  
## <a name="setting-web-part-properties"></a>Definindo propriedades da Web Part  
 Uma Web Part tem propriedades personalizadas usadas para configurar a funcionalidade específica. Uma Web Part também tem propriedades comuns que são padrão para toda Web Part.  
  
### <a name="change-default-properties"></a>Alterar propriedades padrão  
 A Web Part do Visualizador de Relatórios tem propriedades padrão idealmente adequadas para abrir relatórios sob demanda a partir de uma biblioteca ou pasta. Por padrão, todos os controles disponíveis são exibidos na barra de ferramentas. Altura e largura são definidos para usarem todo o espaço disponível na página da Web. Se quiser modificar as propriedades padrão, poderá personalizar a Web Part com as **Configurações de Site**.  
  
1.  No menu **Ações do Site** , clique em **Configurações de Site**.  
  
2.  Em Galerias, clique em **Web parts**.  
  
3.  Clique em **ReportViewer.dwp**.  
  
4.  Abra o painel de ferramentas e defina as propriedades que deseja usar.  
  
### <a name="customize-an-embedded-report-viewer-in-a-web-page"></a>Personalizar um Visualizador de Relatórios inserido em uma página da Web  
 Você pode definir as propriedades para ajustar o Visualizador de Relatórios em uma página da Web. O Visualizador de Relatórios pode usar o mesmo estilo e cores que a página que o contém. Você pode ocultar toda ou parte da barra de ferramentas, o mapa do documento e a área de parâmetros para maximizar a área de exibição do relatório no espaço alocado. O relatório sempre usa os estilos definidos para ele quando ele foi criado; você não pode personalizar a aparência do relatório depois de publicá-lo em uma biblioteca do SharePoint.  
  
 Se estiver inserindo a Web Part do Visualizador de Relatórios em uma página da Web, você deve definir a propriedade **URL de Relatório** para um relatório especificado. Se não estiver, o Visualizador de Relatórios exibirá instruções para vincular a um relatório. Você não pode personalizar nem remover as instruções.  
  
### <a name="custom-properties-of-the-report-viewer-web-part"></a>Propriedades personalizadas da Web Part do Visualizador de Relatórios  
 Ao definir propriedades personalizadas, verifique se algumas propriedades são usadas somente quando a Web Part do Visualizador de Relatórios está inserida em uma página. Os exemplos incluem Título, Altura, Largura, Tipo de cromado e Zona. Outras propriedades, como as configurações da Barra de Ferramentas e Parâmetros, são usadas independentemente de o Visualizador de Relatórios aparecer em uma página ou abrir um relatório em modo de página inteira.  
  
 As propriedades personalizadas da Web Part do Visualizador de Relatórios são listadas a seguir.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|Relatório|Um caminho totalmente qualificado para um relatório que esteja no site do SharePoint atual ou em um site no mesmo aplicativo Web ou farm. Para obter os melhores resultados ao definir propriedades adicionais, clique em Aplicar depois de especificar a URL do relatório.|  
|Destino do Hiperlink|HTML padrão que especifica o quadro de destino para exibir conteúdo vinculado no documento atual. Para relatórios que incluem hiperlinks para sites externos, você pode especificar se um documento de destino substitui o relatório existente dentro da janela atual ou se ele é aberto em uma nova janela do navegador. Os valores válidos incluem `_Top`, `_Blank` e `_Self`. `_Top` usa a janela atual, `_Blank` carrega o documento em uma nova janela do navegador e `_Self` abre o documento dentro do quadro atual. Embora `_Parent` seja um valor válido para o atributo Target em HTML, ele não deve ser usado para uma Web Part do Visualizador de Relatórios inserida em uma página.|  
|Gerar automaticamente o título da Web Part|Um título gerado que inclui o nome da Web Part do Visualizador de Relatórios e o nome do relatório, separados por um traço. Se o relatório não tiver um título, será usado o nome do arquivo do relatório. O título fica visível quando você adiciona uma Web Part a uma página. Se essa caixa de seleção estiver marcada, o título será gerado sempre que a página for atualizada.|  
|Gerar automaticamente o link de detalhes da Web Part|Um hiperlink gerado que é exibido acima da Web Part. Você pode clicar no link para abrir o relatório em uma nova página, em modo de página inteira.|  
|Mostrar item de menu do construtor de relatórios|Mostra ou oculta a opção de menu **Ações** para abrir o Construtor de Relatórios.|  
|Mostrar item de menu de assinatura|Mostra ou oculta a opção de menu **Ações** para criar uma assinatura para o relatório.|  
|Mostrar item do menu imprimir|Mostra ou oculta a opção de menu **Ações** para imprimir o relatório.|  
|Mostrar item do menu exportar|Mostra ou oculta a opção de menu **Ações** para exportar o relatório.|  
|Mostrar botão atualizar|Mostra ou oculta o botão atualizar na barra de ferramentas.|  
|Mostrar controles de navegação de página|Mostra ou oculta os botões de navegação de relatório na barra de ferramentas. Esta opção altera a visibilidade de todos os controles de navegação.|  
|Mostrar botão voltar|Mostra ou oculta o botão voltar na barra de ferramentas.|  
|Mostrar controles de localização|Mostra ou oculta os controles de localização na barra de ferramentas. Esses controles permitem que um usuário procure texto no relatório renderizado. Esta opção altera a visibilidade de todos os controles de localização.|  
|Mostrar controle de zoom|Mostra ou oculta o controle de zoom na barra de ferramentas.|  
|Mostrar botão feed ATOM|Mostra ou oculta o botão feed ATOM na barra de ferramentas.<br /><br /> ![htmlviewer_datafeed](media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|  
|Localização da Barra de Ferramentas|Determina o local da barra de ferramentas dentro do visualizador de relatórios. Os valores válidos incluem `Top` e `Bottom`.|  
|Área de prompt|Os valores válidos incluem `Displayed`, `Collapsed` e `Hidden`. `Displayed` é exibido na área Parâmetros para os relatórios que incluem valores com parâmetros e que exigem a entrada do usuário antes de o relatório ser executado. Use `Hidden` se todos os parâmetros do relatório estiverem especificados e você não quiser que a área de parâmetros fique visível para os usuários.|  
|Largura da Área de Parâmetros|Você pode escolher a medida e o valor. O padrão é 200 pixels. A única exigência desta propriedade é que o valor seja maior do que zero.|  
|Mapa do documento|Um controle de navegação definido em um relatório e usado para fornecer acesso com um único clique a seções específicas do relatório. Ele está disponível em relatórios HTML. O mapa do documento é exibido em uma área recolhível ao lado da área de exibição do relatório. Os valores válidos incluem `Displayed`, `Collapsed` e `Hidden`. Se um mapa do documento estiver definido para um relatório, a área será expandida por padrão a menos que seja marcada como oculta ou recolhida nas propriedades da Web Part. Se o mapa do documento estiver recolhido, você poderá clicar na seta para expandi-lo.|  
|Largura da Área de Mapa do Documento|Você pode escolher a medida e o valor. O padrão é 200 pixels. A única exigência desta propriedade é que o valor seja maior do que zero.|  
|Carregar Parâmetros|Recupera as propriedades dos parâmetros do relatório. Nem todos os relatórios têm parâmetros. Se o relatório não tiver parâmetros, nenhum valor será retornado. Se você estiver definindo propriedades de um relatório recém-carregado, poderá receber um erro indicando que a conexão da fonte de dados foi excluída. Se isso acontecer, redefina a conexão e termine de definir as propriedades dos parâmetros depois que a conexão for especificada. Para obter mais informações sobre como definir a conexão, consulte [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).<br /><br /> Para obter os melhores resultados, clique em **Aplicar** antes de clicar em Carregar Parâmetros.<br /><br /> Depois de carregar as propriedades dos parâmetros, você poderá defini-las da mesma maneira como faria nas páginas de propriedades de parâmetros do relatório. Para obter mais informações sobre como definir parâmetros, consulte [Definir parâmetros em um relatório publicado &#40;Reporting Services no modo integrado do SharePoint&#41;](report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).|  
  
## <a name="customizing-the-toolbar"></a>Personalizando a caixa de ferramentas  
 A barra de ferramentas é exibida abaixo do título e abrange a parte superior do relatório. Ela proporciona o menu **Ações** , a navegação de página para relatórios paginados, atualização e zoom. Também inclui um controle de mapa do documento para relatórios que têm um mapa do documento. O menu **Ações** inclui comandos para exportar o relatório, procurar texto ou números no relatório, imprimir o relatório e abrir o relatório no Construtor de Relatórios.  
  
 Não é possível adicionar novos comandos ao menu  **Ações** , mas é possível personalizá-lo alterando as opções que ficam visíveis para os usuários. Para alterar a visibilidade dos botões e controles da barra de ferramentas, altere as opções da seção **Visibilidade de Itens da Barra de Ferramentas** da Web Part. Também é possível remover apenas o comando **Imprimir** ou formatos de exportação específicos tornando esses recursos não disponíveis no servidor de relatório. Os controles de navegação de página estão disponíveis para relatórios que têm quebras de página; caso contrário, o relatório é uma única página de comprimento variável. **Atualizar** reprocessa o relatório usando os parâmetros atuais. Para exibir todos os controles em uma linha, defina a largura geral da Web Part até pelo menos 400 pixels.  
  
## <a name="customizing-the-viewing-area"></a>Personalizando a área de exibição  
 A área de exibição é usada para exibir relatórios. A área de exibição de relatório é compartilhada com as áreas Parâmetros e Credenciais, se elas forem usadas. Se forem necessárias credenciais, a área Credenciais será exibida ao lado de uma área de exibição de relatório em branco. A área Credenciais é fechada depois que o usuário fornecer credenciais e executar o relatório. Para personalizar o texto que pede aos usuários para definir credenciais, modifique as propriedades de conexão da fonte de dados. Para obter mais informações, consulte [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
 A área Parâmetros fornece campos para digitar valores antes de executar o relatório. Ela só é usada quando a definição de um relatório inclui parâmetros. Quando as áreas Parâmetros ou Credenciais são exibidas, a exibição do relatório é ajustada para usar a largura restante da Web Part. Você pode definir propriedades na Web Part para personalizar a largura da área Parâmetros. Também pode definir os rótulos exibidos ao lado dos parâmetros individuais na página. Para obter mais informações sobre como modificar rótulos de parâmetros, consulte [Definir parâmetros em um relatório publicado &#40;Reporting Services no modo integrado do SharePoint&#41;](report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Consulte também  
 [Web Part do Visualizador de Relatórios em um site do SharePoint](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Adicionar a Web Part do Visualizador de Relatórios a uma página da Web &#40;Reporting Services no modo integrado do SharePoint&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
