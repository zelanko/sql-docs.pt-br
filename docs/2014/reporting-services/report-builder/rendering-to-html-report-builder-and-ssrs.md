---
title: Renderizando para HTML (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: cf559b0a-499a-4d74-b520-b382b87e0b17
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 83485916e0dcfeb02555e3068931415801691692
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296844"
---
# <a name="rendering-to-html-report-builder-and-ssrs"></a>Renderizando para HTML (Construtor de Relatórios e SSRS)
  A extensão de renderização HTML renderiza um relatório no formato HTML. A extensão de renderização também pode produzir páginas HTML totalmente formadas ou fragmentos de HTML a serem inseridos em outras páginas HTML. Todo o HTML é gerado com a codificação UTF-8.  
  
 A extensão de renderização HTML é a extensão de renderização padrão para relatórios que são exibidos em um navegador, incluindo quando executados no Gerenciador de Relatórios.  
  
 A extensão de renderização HTML é a extensão de renderização padrão para relatórios que são exibidos em um navegador, incluindo quando executados no Gerenciador de Relatórios. A extensão de renderização HTML pode renderizar HTML como um fragmento ou como um documento HTML completo. Se o MHTML for um fragmento, as marcas `HEAD`, `HTML` e `BODY` do documento HTML serão removidas. Apenas o conteúdo da marca `BODY` é processado. Isso é útil para inserir o HTML no HTML produzido por outro aplicativo.  
  
 Em alguns cenários, parâmetros de relatório podem ser usados para iniciar ataques de injeção de script durante a renderização de relatórios em HTML. Para obter mais informações sobre como proteger relatórios, consulte [Protegendo Relatórios e Recursos](../security/secure-reports-and-resources.md).  
  
 Para obter mais informações sobre navegadores, consulte [Planning for Reporting Services e o suporte a navegador Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RenderingMHTML"></a> Renderizando em MHTML  
 A extensão de renderização HTML também pode renderizar relatórios em MHTML (encapsulamento MIME de documentos HTML agregados). O MHTML estende o HTML para inserir objetos codificados, como imagens, no documento HTML. Usando a extensão de renderização MHTML, você pode inserir recursos, como imagens, documentos ou outros arquivos binários, como estruturas MIME, no relatório HTML, em um único arquivo. Os relatórios MHTML também são úteis para serem inseridos em mensagens de email, pois todos os recursos estão incluídos no relatório. Embora na verdade seja a extensão de renderização HTML que renderiza o MHTML, esse recurso também pode ser referido como a extensão de renderização MHTML.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="BrowserSupport"></a> Suporte do navegador  
 Essa extensão de renderização oferece suporte às seguintes versões de navegador:  
  
-   Internet Explorer 5.5 e posterior  
  
-   Firefox 1.5 e posterior  
  
-   Safari 3.0 e posterior  
  
 Devido a considerações de navegador cruzadas, o relatório renderizado pode variar ligeiramente do navegador para navegador. Por exemplo, a caixa de texto contém uma propriedade chamada WritingMode. O Firefox não oferece suporte a essa propriedade.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="HTMLSpecificRenderingRules"></a> HTML - Regras específicas de renderização  
 As seguintes regras específicas de HTML são aplicadas ao renderizar:  
  
-   O processador cria uma estrutura de tabela HTML para conter todos os itens em cada coleção de `ReportItems`, se houver mais de uma.  
  
-   Todo item na estrutura da tabela ocupa uma única célula.  
  
-   Células vazias são recolhidas juntas o máximo possível para reduzir o tamanho do HTML.  
  
-   Uma linha de células vazias é adicionada à borda superior e outra coluna à borda esquerda para melhorar a velocidade na qual os navegadores podem renderizar a tabela.  
  
-   São atribuídas larguras e alturas fixas às colunas ou linhas da tabela que não contêm itens, somente lacunas entre os itens.  
  
-   Todas as outras linhas e colunas têm permissão para crescer, dependendo do tamanho de cada item de relatório.  
  
-   Todas as coordenadas e tamanhos de item de relatório são convertidos para milímetros. Todos os outros tamanhos, inclusive propriedades de estilo, retêm suas unidades originais. Diferenças de tamanho e posição menores que 0,2 mm são tratadas como 0 mm.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="Interactivity"></a> Interatividade  
 Alguns elementos interativos têm suporte em HTML. A seguir, uma descrição dos comportamentos específicos.  
  
### <a name="show-and-hide"></a>Mostrar e Ocultar  
 Um item de relatório cuja visibilidade pode ser alternada é renderizado com uma imagem de alternância de +/- e pode ser clicada. Quando o item é clicado, ocorre um retorno de chamada ao servidor para que ele renderize novamente a saída com o estado mostrar ou ocultar alterado.  
  
### <a name="document-map"></a>Mapa do documento  
 Os rótulos do mapa do documento são renderizados e podem ser navegados usando o mapa do documento no controle do visualizador. Para cabeçalhos de região de dados omitidos, os rótulos são renderizados na primeira célula filho. Se não houver nenhuma célula filho presente, o rótulo será renderizado na filho que a antecede.  
  
### <a name="bookmarks"></a>Indicadores  
 Links de indicadores são renderizados e são exibidos como hyperlinks. Destinos de indicadores são renderizados e podem ser navegados, clicando nos links de indicadores. Quando um link de indicador é clicado, o relatório vai para a primeira ocorrência do rótulo do indicador de destino e, quando possível, o navegador é rolado para que o link do indicador fique na parte superior da janela. As marcações de âncora de HTML (\<a>) são usadas para marcar destinos de indicadores.  
  
### <a name="interactive-sorting"></a>Classificação interativa  
 Se uma caixa de texto tiver uma classificação de usuário definida, a extensão de renderização HTML renderizará os ícones de classificação na caixa de texto à direita do conteúdo. Se um relatório contiver qualquer caixa de texto na qual a classificação do usuário está definida, o JavaScript será renderizado, gerando um “postback” para o servidor quando a imagem de classificação for clicada.  
  
### <a name="hyperlinks-and-drillthrough"></a>Hyperlinks e detalhamento  
 Os hiperlinks e links de detalhamento são renderizados como hiperlinks em itens de relatório usando as marcações de âncora HTML (\<a>) ao redor do item no qual elas estão definidas.  
  
### <a name="search"></a>Pesquisa  
 O recurso Pesquisar permite que os usuários procurem uma cadeia de caracteres de texto no relatório.  
  
 Uma funcionalidade adicional de pesquisa e localização é fornecida pelo controle Web Forms do ReportViewer.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="DeviceInfo"></a> Configurações de informações de dispositivo  
 Você pode alterar algumas configurações padrão para este processador, incluindo qual modo deve ser renderizado, alterando as configurações de informações de dispositivo: Para obter mais informações, consulte [Configurações de informações do dispositivo HTML](../html-device-information-settings.md).  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
## <a name="see-also"></a>Consulte também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
