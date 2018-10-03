---
title: Layout da página e renderização (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e2358653-35bc-4496-810a-d3ccf02f229f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 99d7bcaf87fec0181392fd8673cb90df37849308
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082826"
---
# <a name="page-layout-and-rendering-report-builder-and-ssrs"></a>Layout de página e renderização (Construtor de Relatórios e SSRS)
  Quando você cria relatórios, é importante compreender o comportamento dos renderizadores do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para garantir que o relatório renderizado tenha a aparência desejada, incluindo o layout de página e as quebras de páginas. Provavelmente, você também deseja ter certeza de que o relatório renderizado se ajusta ao tamanho do papel geralmente usado na sua organização.  
  
 Quando você exibe relatórios no Gerenciador de Relatórios ou no painel de visualização do Construtor de Relatórios ou o Designer de Relatórios, o relatório é renderizado primeiro pelo renderizador HTML. Você pode exportar o relatório então para formatos diferentes, como Excel ou CSV. O relatório exportado pode ser usado então para análise adicional no Excel ou como fonte de dados para aplicativos que podem importar e usar arquivos de dados CSV.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui um conjunto de renderizadores para exportar relatórios para formatos diferentes. Cada renderizador aplica regras ao renderizar relatórios. Quando você exporta um relatório para um formato de arquivo diferente, principalmente para renderizadores como o Adobe Acrobat (PDF), que usa paginação com base no tamanho de página físico, talvez seja necessário alterar o layout de seu relatório para que o relatório exportado pareça e seja impresso corretamente após a aplicação das regras de renderização.  
  
 A obtenção dos melhores resultados para relatórios exportados é frequentemente um processo iterativo; você cria e visualiza o relatório no Construtor de Relatórios ou no Designer de Relatórios, exporta o relatório para o formato de sua preferência, examina o relatório exportado e faz as alterações no relatório.  
  
 Este tópico fornece informações sobre as extensões de renderização do Reporting Services e como trabalhar com elas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="PageLayout"></a> Layout de página e itens de relatório  
 Os itens de relatório são elementos de layout que são associados a diferentes tipos de dados de relatório. Tabela, matriz, lista, gráfico e medidor são itens de relatório da região de dados que se vinculam a um conjunto de dados de relatório. Quando o relatório é processado, a região de dados é expandida para cima e para baixo da página de relatório para exibir dados. Outros itens de relatório são vinculados e exibem um item simples. Um item de relatório **Imagem** é vinculado a uma imagem. Um item de relatório **Caixa de Texto** contém texto simples, como um título ou uma expressão que pode incluir referências a campos internos, parâmetros de relatório ou campos do conjunto de dados. Os itens de relatório **Linha** e **Retângulo** fornecem elementos gráficos simples para a página do relatório. O **Retângulo** também pode ser um contêiner para outros itens de relatório. Um relatório pode conter sub-relatórios.  
  
 Com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode colocar itens de relatório em qualquer local na superfície de design. De maneira interativa, é possível colocar, expandir e assumir a forma inicial do item de relatório usando linhas ajustadas e redimensionando alças. Você poderá colocar regiões de dados com diferentes conjuntos de dados ou até os mesmos dados em diferentes formatos, lado a lado. Ao colocar um item de relatório na superfície de design, ele apresenta tamanho, forma e relação inicial padrão com relação a todos os outros itens de relatório. Você pode colocar muitos itens de relatório um ao outro criar mais designs de relatório complexos. Por exemplo, traça um gráfico ou imagens em células de tabela, tabelas em células de tabela e várias imagens em um retângulo. Além de fornecer a organização e olha você deseja no relatório, colocando itens de relatório em contêineres como retângulos ajuda controlar o modo que os itens de relatório são exibidos na página de relatório.  
  
 Um relatório pode ajustar várias páginas, com cabeçalho e rodapé iguais em cada uma das páginas. Além disso, um relatório pode conter elementos gráficos, como imagens e linhas, além de várias fontes, cores e estilos que podem ter como base as expressões.  
  
##  <a name="ReportSections"></a> Seções do relatório  
 Um relatório é formado por três seções principais: um cabeçalho de página opcional, um rodapé de página opcional e um corpo para a mensagem. O cabeçalho e o rodapé do relatório não são seções separadas do relatório, mas fazem parte dos itens de relatório que são colocados na parte superior e inferior do corpo do relatório. O cabeçalho e o rodapé repetem o mesmo conteúdo na parte superior e inferior de cada página do relatório. Você pode colocar imagens, caixas de texto e linhas em cabeçalhos e rodapés. Todos os tipos de itens de relatório podem ser colocados no corpo do relatório.  
  
 Você também pode definir propriedades nos itens de relatório para inicialmente ocultá-los ou mostrá-los na página. As propriedades de visibilidade podem ser definidas em linhas, colunas ou grupos para regiões de dados e fornecer botões de alternância, permitindo ao usuário mostrar ou ocultar os dados do relatório de maneira interativa. Também é possível definir a visibilidade ou a visibilidade inicial usando expressões, inclusive expressões baseadas em parâmetros de relatórios.  
  
 Quando um relatório é processado, os dados do relatório são combinados com os elementos de layout do relatório e os dados combinados são enviados para um processador de relatórios. O processador segue regras predefinidas de item de expansão e determina a quantidade de dados que será ajustada em cada página. Para desenvolver com êxito um relatório que seja lido facilmente e que seja otimizado para o processador que você pretende usar, é preciso compreender as regras usadas para controlar a paginação no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter mais informações, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
##  <a name="RenderingExtensions"></a> Renderizadores  
 O Reporting Services inclui um conjunto de renderizadores, também chamado extensões de renderização, que você pode usar para exportar relatórios para formatos diferentes. Há três tipos de renderizadores:  
  
-   **Renderizadores de dados** Os renderizadores de dados eliminam todas as informações de formatação e layout do relatório e exibem apenas os dados. O arquivo resultante pode ser usado para importar os dados brutos do relatório para outro tipo de arquivo, como o Excel, ou outro banco de dados, como uma mensagem de dados XML ou um aplicativo personalizado. Os renderizadores de dados disponíveis são: CSV e XML.  
  
    > [!NOTE]  
    >  Embora não forneça exportação direta para um formato diferente, a renderização Atom gera arquivos de dados com base em relatórios.  
  
-   **Renderizadores de quebra de página flexível** Os renderizadores de quebra de página flexível mantêm o layout e a formatação do relatório. O arquivo resultante é otimizado para exibição e entrega com base na tela, como em uma página da Web. Os renderizadores de quebra de página flexível disponíveis são: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word, o arquivo da Web (MHTML) e HTML.  
  
-   **Renderizadores de quebra de página não flexíveis** Os renderizadores de quebra de página não flexíveis mantêm o layout e a formatação do relatório. O arquivo resultante é otimizado para uma experiência consistente de impressão, ou para exibir o relatório online em formato de um livro. Os renderizadores de quebra de página não flexíveis disponíveis têm suporte: TIFF e PDF.  
  
 Quando você visualiza um relatório no Construtor de Relatórios ou no Designer de Relatórios, ou executa um relatório no Gerenciador de Relatórios, ele é sempre renderizado primeiro em HTML. Depois que executar o relatório, é possível exportá-lo para diversos formatos de arquivo. Para obter mais informações, consulte [exportando relatórios &#40;construtor de relatórios e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md).  
  
  
  
##  <a name="RenderingBehaviors"></a> Comportamentos de renderização  
 Dependendo do renderizador selecionado, algumas regras são aplicadas durante a renderização do relatório. Como os itens de relatório são ajustados juntos em uma página é determinado pela combinação destes fatores:  
  
-   Renderizando regras.  
  
-   A largura e altura dos itens de relatório.  
  
-   O tamanho do corpo do relatório.  
  
-   A largura e altura da página.  
  
-   Suporte específico do renderizador para paginação.  
  
 Por exemplo, os relatórios renderizados para formatos HTML e MHTML são otimizados para uma experiência baseada em telas de computador em que as páginas podem ter vários comprimentos.  
  
 Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
  
  
##  <a name="Pagination"></a> Paginação  
 A paginação se refere ao número de páginas dentro de um relatório e ao modo como os itens de relatório são organizados nessas páginas. A paginação no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] varia, dependendo da extensão de renderização que você usa para exibir e entregar o relatório e das opções de quebra de página e keep-together configuradas para uso do relatório.  
  
 Para desenvolver com êxito um relatório que seja facilmente lido pelos seus usuários bem como que seja otimizado para o processador que pretende usar na entrega do relatório, você deve entender as regras utilizadas para controlar a paginação no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Os relatórios exportados com o uso dos dados e extensões de renderização de página flexível na memória não são afetados geralmente pela paginação. Quando você usa uma extensão de renderização de dados, o relatório é renderizado como conjunto de linhas de tabela no formato XML ou CSV. Para assegurar que os dados de relatório exportados sejam utilizáveis, você deve entender as regras aplicadas para renderizar um conjunto de linhas de tabela mescladas de um relatório.  
  
 Ao usar uma extensão de renderização de página flexível, como a extensão de renderização HTML, talvez você queira saber qual a aparência do relatório quando impresso e também como ele será renderizado usando um renderizador de página de não flexível como PDF. Durante a criação ou a atualização de um relatório você pode visualizá-lo e exportá-lo no Construtor de Relatórios e no Designer de Relatórios.  
  
 Os renderizadores de página de hardware têm o maior impacto no layout do relatório e o tamanho de página física. Para saber mais, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção lista procedimentos que mostram a você, passo a passo, como trabalhar com a paginação em relatórios.  
  
-   [Adicionar uma quebra de página &#40;relatórios e SSRS&#41;](add-a-page-break-report-builder-and-ssrs.md)  
  
-   [Exibir cabeçalhos de linhas e colunas em várias páginas &#40;relatórios e SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)  
  
-   [Adicionar ou remover um cabeçalho ou rodapé de &#40;relatórios e SSRS&#41;](add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)  
  
-   [Manter os cabeçalhos visíveis ao rolar por um relatório &#40;relatórios e SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
-   [Exibir números de página ou outras propriedades de relatório &#40;relatórios e SSRS&#41;](display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)  
  
-   [Ocultar um cabeçalho ou rodapé na primeira ou na última página &#40;relatórios e SSRS&#41;](hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)  
  
  
  
##  <a name="InThisSection"></a> Nesta seção  
 Os tópicos a seguir fornecem informações adicionais sobre layout e renderização de página.  
  
 [Cabeçalhos e rodapés de página &#40;relatórios e SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)  
 Fornece informações sobre como usar cabeçalhos e rodapés em relatórios e como controlar a paginação usando esses recursos.  
  
 [Controlando quebras de páginas, títulos, colunas e linhas &#40;relatórios e SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)  
 Fornece informações sobre como usar quebras de página.  
  
  
  
## <a name="see-also"></a>Consulte também  
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;relatórios e SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Exportando relatórios &#40;relatórios e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
