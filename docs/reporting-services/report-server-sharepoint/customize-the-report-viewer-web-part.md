---
title: "Personalizar a web part do Visualizador de relatórios | Microsoft Docs"
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 38f23cf5d75c47be55e1820a4421a507a73df54e
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="customize-the-report-viewer-web-part"></a>Personalizar a web part do Visualizador de relatórios

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Você pode usar a web part do Visualizador de relatórios para exibir relatórios executados em um servidor de relatório está configurado para integração do SharePoint. Os relatórios que você pode exibir incluem arquivos de definição de relatório (.rdl) e relatórios do Construtor de Relatórios. Os relatórios são abertos na web part do Visualizador de relatórios em uma nova página automaticamente, mas você também pode adicionar uma web part do Visualizador de relatórios para uma página da web existente ou um site se você quiser que um determinado relatório sempre esteja visível nessa página.

> [!NOTE]
> Embora tenham nomes idênticos, o Visualizador de relatórios da web part que é instalado por meio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento é diferente da web part do Visualizador de relatórios que está incluída no arquivo RSWebParts.cab. As instruções neste tópico são específicas para a web part do Visualizador de relatórios que é instalada por meio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento.

 Você pode personalizar a web part do Visualizador de relatórios das seguintes maneiras:  
  
-   Altere a aparência da web part definindo propriedades.  
  
-   Escolha quais recursos de relatórios interativos estão disponíveis na barra de ferramentas do relatório.  
  
-   Especifique quais áreas de exibição estão disponíveis. A web part do Visualizador de relatórios tem uma área de exibição de relatório, uma área de parâmetros e uma área de credenciais.  
  
 Você não pode estender a web part do Visualizador de relatórios para oferecer suporte a diferentes tipos de arquivo, e você não pode substituir a barra de ferramentas do relatório com uma barra de ferramentas personalizada ou adicionar nova funcionalidade à barra de ferramentas existente. Se você precisar de personalização de recursos padrão, você deve criar uma parte da web personalizado.  

## <a name="setting-web-part-properties"></a>Definindo propriedades da web part

 Uma web part tem propriedades personalizadas que são usadas para configurar a funcionalidade específica. Uma web part também tem propriedades comuns que são padrão para cada web part.  
  
### <a name="change-default-properties"></a>Alterar propriedades padrão

 A web part do Visualizador de relatórios tem propriedades padrão que são ideais para abrir relatórios sob demanda a partir de uma biblioteca ou pasta. Por padrão, todos os controles disponíveis são exibidos na barra de ferramentas e altura e largura são definidos para usar todo o espaço disponível na página da web. Se você quiser modificar as propriedades padrão, você pode personalizar a web part com **configurações do Site**.  
  
1.  No menu **Ações do Site** , clique em **Configurações de Site**.  
  
2.  Em galerias, clique em **web parts**.  
  
3.  Clique em **ReportViewer.dwp**.  
  
4.  Abra o painel de ferramentas e defina as propriedades que deseja usar.  
  
### <a name="customize-an-embedded-report-viewer-in-a-web-page"></a>Personalizar um visualizador de relatório inserido em uma página da web

 Você pode definir propriedades para ajustar o Visualizador de relatórios em uma página da web. O Visualizador de Relatórios pode usar o mesmo estilo e cores que a página que o contém. Você pode ocultar toda ou parte da barra de ferramentas, o mapa do documento e a área de parâmetros para maximizar a área de exibição do relatório no espaço alocado. O relatório sempre usa os estilos definidos para ele quando ele foi criado; você não pode personalizar a aparência do relatório depois de publicá-lo em uma biblioteca do SharePoint.  
  
 Se você estiver inserindo a web part do Visualizador de relatórios em uma página da web, você deve definir o **URL de relatório** propriedade a um relatório específico. Se não estiver, o Visualizador de Relatórios exibirá instruções para vincular a um relatório. Você não pode personalizar nem remover as instruções.  
  
### <a name="custom-properties-of-the-report-viewer-web-part"></a>Propriedades personalizadas da web part do Visualizador de relatórios

 Ao definir propriedades personalizadas, lembre-se de que algumas propriedades são usadas somente quando a web part do Visualizador de relatórios está inserida em uma página. Os exemplos incluem Título, Altura, Largura, Tipo de cromado e Zona. Outras propriedades, como as configurações da Barra de Ferramentas e Parâmetros, são usadas independentemente de o Visualizador de Relatórios aparecer em uma página ou abrir um relatório em modo de página inteira.  
  
 As propriedades personalizadas da web part do Visualizador de relatórios estão listadas abaixo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|Relatório|Um caminho totalmente qualificado para um relatório que esteja no site do SharePoint atual ou em um site no mesmo aplicativo Web ou farm. Para obter os melhores resultados ao definir propriedades adicionais, clique em Aplicar depois de especificar a URL do relatório.|  
|Destino do Hiperlink|HTML padrão que especifica o quadro de destino para exibir conteúdo vinculado no documento atual. Para relatórios que incluem hiperlinks para sites externos, você pode especificar se um documento de destino substitui o relatório existente dentro da janela atual ou se ele é aberto em uma nova janela do navegador. Os valores válidos incluem **_Top**, **_Blank**, e **_Self**. **_Top** usa a janela atual, **_Blank** carrega o documento em uma nova janela do navegador e **_Self** abre o documento dentro do quadro atual. Embora **Parent** é um valor válido para o atributo Target em HTML, ele não usado de uma web part do Visualizador de relatórios que é inserida em uma página.|  
|Gerar automaticamente a web part do título|Um título gerado que inclui o nome da web part do Visualizador de relatórios e o nome do relatório, separados por um traço. Se o relatório não tiver um título, será usado o nome do arquivo do relatório. O título fica visível quando você adiciona uma web part a uma página. Se essa caixa de seleção estiver marcada, o título será gerado sempre que a página for atualizada.|  
|Gerar automaticamente a web part de Link de detalhes|Um hiperlink gerado que aparece acima da web part. Você pode clicar no link para abrir o relatório em uma nova página, em modo de página inteira.|  
|Mostrar item de menu do construtor de relatórios|Mostra ou oculta a opção de menu **Ações** para abrir o Construtor de Relatórios.|  
|Mostrar item de menu de assinatura|Mostra ou oculta a opção de menu **Ações** para criar uma assinatura para o relatório.|  
|Mostrar item do menu imprimir|Mostra ou oculta a opção de menu **Ações** para imprimir o relatório.|  
|Mostrar item do menu exportar|Mostra ou oculta a opção de menu **Ações** para exportar o relatório.|  
|Mostrar botão atualizar|Mostra ou oculta o botão atualizar na barra de ferramentas.|  
|Mostrar controles de navegação de página|Mostra ou oculta os botões de navegação de relatório na barra de ferramentas. Esta opção altera a visibilidade de todos os controles de navegação.|  
|Mostrar botão voltar|Mostra ou oculta o botão voltar na barra de ferramentas.|  
|Mostrar controles de localização|Mostra ou oculta os controles de localização na barra de ferramentas. Esses controles permitem que um usuário procure texto no relatório renderizado. Esta opção altera a visibilidade de todos os controles de localização.|  
|Mostrar controle de zoom|Mostra ou oculta o controle de zoom na barra de ferramentas.|  
|Mostrar botão feed ATOM|Mostra ou oculta o botão feed ATOM na barra de ferramentas.<br /><br /> ![htmlviewer_datafeed](../../reporting-services/media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|  
|Localização da Barra de Ferramentas|Determina o local da barra de ferramentas dentro do visualizador de relatórios. Os valores válidos incluem **Top** e **Bottom**.|  
|Área de prompt|Os valores válidos incluem **Displayed**, **Collapsed**e **Hidden**. **Displayed** é exibido na área Parâmetros para os relatórios que incluem valores com parâmetros e que exigem a entrada do usuário antes de o relatório ser executado. Use **Hidden** se todos os parâmetros do relatório estiverem especificados e você não quiser que a área de parâmetros fique visível para os usuários.|  
|Largura da Área de Parâmetros|Você pode escolher a medida e o valor. O padrão é 200 pixels. A única exigência desta propriedade é que o valor seja maior do que zero.|  
|Mapa do documento|Um controle de navegação definido em um relatório e usado para fornecer acesso com um único clique a seções específicas do relatório. Ele está disponível em relatórios HTML. O mapa do documento é exibido em uma área recolhível ao lado da área de exibição do relatório. Os valores válidos incluem **Displayed**, **Collapsed**e **Hidden**. Se um mapa do documento estiver definido para um relatório, a área será expandida por padrão, a menos que marcada como oculta ou recolhida nas propriedades da web part. Se o mapa do documento estiver recolhido, você poderá clicar na seta para expandi-lo.|  
|Largura da Área de Mapa do Documento|Você pode escolher a medida e o valor. O padrão é 200 pixels. A única exigência desta propriedade é que o valor seja maior do que zero.|  
|Carregar Parâmetros|Recupera as propriedades dos parâmetros do relatório. Nem todos os relatórios têm parâmetros. Se o relatório não tiver parâmetros, nenhum valor será retornado. Se você estiver definindo propriedades de um relatório recém-carregado, poderá receber um erro indicando que a conexão da fonte de dados foi excluída. Se isso acontecer, redefina a conexão e termine de definir as propriedades dos parâmetros depois que a conexão for especificada. Para obter mais informações sobre como definir a conexão, consulte [&#40; de criar e gerenciar fontes de dados compartilhadas O Reporting Services no SharePoint integrado modo &#41; ](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).<br /><br /> Para obter os melhores resultados, clique em **Aplicar** antes de clicar em Carregar Parâmetros.<br /><br /> Depois de carregar as propriedades dos parâmetros, você poderá defini-las da mesma maneira como faria nas páginas de propriedades de parâmetros do relatório. Para obter mais informações sobre como definir parâmetros, consulte [definir parâmetros em um relatório publicado &#40; O Reporting Services no SharePoint integrado modo &#41; ](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).|  

## <a name="customizing-the-toolbar"></a>Personalizando a barra de ferramentas

 A barra de ferramentas é exibida abaixo do título e abrange a parte superior do relatório. Ela proporciona o menu **Ações** , a navegação de página para relatórios paginados, atualização e zoom. Também inclui um controle de mapa do documento para relatórios que têm um mapa do documento. O menu **Ações** inclui comandos para exportar o relatório, procurar texto ou números no relatório, imprimir o relatório e abrir o relatório no Construtor de Relatórios.  
  
 Não é possível adicionar novos comandos ao menu  **Ações** , mas é possível personalizá-lo alterando as opções que ficam visíveis para os usuários. Para alterar a visibilidade dos botões de barra de ferramentas e controles, você pode alterar opções no **visibilidade de itens da barra de ferramentas** seção da web part. Também é possível remover apenas o comando **Imprimir** ou formatos de exportação específicos tornando esses recursos não disponíveis no servidor de relatório. Os controles de navegação de página estão disponíveis para relatórios que têm quebras de página; caso contrário, o relatório é uma única página de comprimento variável. **Atualizar** reprocessa o relatório usando os parâmetros atuais. Para exibir todos os controles em uma linha, defina a largura geral da web part até pelo menos 400 pixels.  

## <a name="customizing-the-viewing-area"></a>Personalizando a área de exibição

 A área de exibição é usada para exibir relatórios. A área de exibição de relatório é compartilhada com as áreas Parâmetros e Credenciais, se elas forem usadas. Se forem necessárias credenciais, a área Credenciais será exibida ao lado de uma área de exibição de relatório em branco. A área Credenciais é fechada depois que o usuário fornecer credenciais e executar o relatório. Para personalizar o texto que pede aos usuários para definir credenciais, modifique as propriedades de conexão da fonte de dados. Para obter mais informações, consulte [&#40; de criar e gerenciar fontes de dados compartilhadas O Reporting Services no SharePoint integrado modo &#41; ](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 A área Parâmetros fornece campos para digitar valores antes de executar o relatório. Ela só é usada quando a definição de um relatório inclui parâmetros. Quando as credenciais ou parâmetros áreas são exibidas, o modo de exibição de relatório é ajustado para usar a largura restante da web part. Você pode definir propriedades na web part para personalizar a largura de parâmetros. Também pode definir os rótulos exibidos ao lado dos parâmetros individuais na página. Para obter mais informações sobre como modificar rótulos de parâmetro, consulte [definir parâmetros em um relatório publicado &#40; O Reporting Services no SharePoint integrado modo &#41; ](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Consulte também

 [Web part do Visualizador de relatórios em um Site do SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Adicionar a web part do Visualizador de relatórios para uma página da web](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
