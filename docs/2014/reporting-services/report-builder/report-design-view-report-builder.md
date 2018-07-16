---
title: Modo de exibição de Design do relatório (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10440"
- "10426"
- "10439"
- "10434"
- "10438"
- "10436"
helpviewer_keywords:
- reports, creating
- user interface
- overview of Report Builder
ms.assetid: 1544472c-2803-448d-af52-e901cb457a00
caps.latest.revision: 20
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 435709e17b917c1b741e1bc619bb1dca106dbd4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244376"
---
# <a name="report-design-view-report-builder"></a>Exibição do design de relatório (Construtor de Relatórios)
  A janela do Construtor de Relatórios foi criada para ajudá-lo a organizar facilmente seus recursos de relatório e criar rapidamente os relatórios de que você precisa. A superfície de design fica no centro da janela, com a Faixa de Opções acima e os painéis Dados do Relatório, Agrupamento e Propriedades, além da Galeria de Partes de Relatório, à esquerda, abaixo e à direita. A superfície de design é o local em que você adiciona e organiza seus itens de relatório. A Faixa de Opções organiza itens de menu tradicionais em categorias que você pode localizar e usar facilmente. Os painéis ajudam a adicionar, selecionar e organizar os recursos de relatório e alteram as propriedades de item de relatório.  
  
 ![ReportDesignView](../media/reportdesignview.gif "ReportDesignView")  
  
##  <a name="Ribbon"></a> A Faixa de Opções  
 A Faixa de Opções foi criada para ajudá-lo a localizar os comandos de que você precisa para executar uma tarefa. Os comandos são organizados em grupos lógicos, que são coletados em conjunto sob guias. Cada guia está relacionada a um tipo de atividade, como a inserção de itens de relatório ou a formatação de texto.  
  
 Na exibição de design de relatório, a Faixa de Opções é dividida nas seguintes guias: Página Inicial, Inserir e Exibir. Se não conseguir localizar uma tarefa na Faixa de Opções, alguns grupos dela têm uma caixa de diálogo relacionada que você pode abrir clicando na seta no canto direito inferior do grupo. Você não pode minimizar ou excluir a Faixa de Opções ou substituí-la por barras de ferramentas e menus.  
  
 No modo de execução, a faixa de opções tem apenas uma guia, **executar**.  
  
### <a name="home-tab"></a>Guia Página Inicial  
 A guia Página Inicial é uma coleção de comandos geralmente usados que enfatiza a aparência dos itens dentro de seu relatório. Na guia Início, você pode acessar os comandos de execução, fonte, parágrafo, borda, número e layout. Quando você clicar em um item na guia, o item selecionado na superfície de design será alterado. Quando você clica em **executar**, o relatório é renderizado em HTML para que você possa ver como o conteúdo do relatório aparecerão quando publicados e você vir a guia execução, em vez da guia página inicial. A guia Início é a guia padrão exibida quando você cria um relatório pela primeira vez.  
  
### <a name="insert-tab"></a>Guia Inserir  
 A guia Inserir é uma coleção de comandos geralmente usados para adicionar itens de relatório ao relatório. Na guia Inserir, você pode usar assistentes para adicionar uma tabela, matriz gráfico ou mapa. Também é possível adicionar esses itens sem usar um assistente e adicionar outros itens de relatório como minigráficos, indicadores, caixas de texto, imagens, linhas, retângulos, sub-relatórios e cabeçalhos e rodapés do relatório.  
  
 Clicando em **partes de relatório** Inserir guia é aberta a Galeria de partes de relatório. Você pode pesquisar partes de relatório salvas em um servidor de relatório. Para obter mais informações, consulte [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
 Após a inserção de um item, o Construtor de Relatórios alterna automaticamente para a guia Página Inicial.  
  
### <a name="view-tab"></a>Guia Exibir  
 A guia Exibir é uma coleção de comandos que controlam o que é exibido dentro da janela do Construtor de Relatórios. Você pode alterar as opções de exibição para a régua e os painéis Agrupamento, Dados de Relatório e Propriedades.  
  
### <a name="run-tab"></a>Guia Executar  
 Quando você clica em **executar** na guia página inicial, você deve executar uma visualização do relatório no Visualizador de HTML e você vir a guia execução, em vez da guia página inicial.  
  
 A guia Executar contém uma coleção de comandos que você pode usar após a renderização do relatório. É possível imprimir o relatório, navegar nas páginas do relatório, exportá-lo para outro formato de arquivo, exibir o mapa do documento ou os parâmetros (caso o relatório tenha) e localizar itens dentro do relatório. Para obter mais informações, consulte [visualizando o relatório no modo de execução](#RunMode).  
  
 Para retornar ao modo de design de relatório na **executados** , clique em **Design**.  
  
  
##  <a name="RptDesignSurface"></a> A superfície de design do relatório  
 A superfície de design de relatório do Construtor de Relatórios é a área de trabalho principal para criar os relatórios. Para colocar itens de relatório, como regiões de dados, sub-relatórios, caixas de texto, imagens, retângulos e linhas no relatório, você os adiciona na Faixa de Opções ou na Galeria de Partes de Relatório à superfície de design. Nela, você pode adicionar grupos, expressões, parâmetros, filtros, ações, visibilidade e formatação a seus itens de relatório.  
  
 Também é possível alterar o seguinte:  
  
-   As propriedades do corpo de relatório, como a borda e a cor de preenchimento, ao clicar com o botão direito do mouse na área branca da superfície de design, fora de qualquer item de relatório, e ao clicar em **Propriedades do Corpo**.  
  
-   As propriedades do cabeçalho e do rodapé, como a borda e a cor de preenchimento, ao clicar com o botão direito do mouse na área branca da superfície de design na área do cabeçalho ou do rodapé, fora de qualquer item de relatório, e ao clicar em **Propriedades do Cabeçalho** ou **Propriedades do Rodapé**.  
  
-   As propriedades do próprio relatório, como a configuração de página, clicando duas vezes na área azul ao redor da superfície de design e clicando em **propriedades do relatório**.  
  
-   As propriedades dos itens de relatório, ao clicar com o botão direito do mouse nelas e ao clicar em **Propriedades**.  
  
> [!NOTE]  
>  Se você arrastar um campo diretamente do painel de dados do relatório para a superfície de design do relatório, em vez de colocá-lo em uma região de dados como uma tabela ou um gráfico, ao executar o relatório, você só verá o primeiro valor dos dados nesse campo.  
  
 Para obter informações sobre como usar o teclado para manipular itens na área de design, consulte [Atalhos de teclado &#40;Construtor de Relatórios&#41;](keyboard-shortcuts-report-builder.md)  
  
### <a name="design-surface-size-and-print-area"></a>Tamanho da superfície de design e área de impressão  
 O tamanho da superfície de design pode ser diferente do tamanho da área de impressão da página que você especifica para imprimir o relatório. A alteração do tamanho da superfície de design não alterará a área de impressão de seu relatório. Não importa que tamanho você definiu para a área de impressão de seu relatório, o tamanho de área de design completo não é alterado. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Para exibir a régua, na guia **Exibir**, marque a caixa de seleção **Régua**.  
  
  
##  <a name="ReptDataPane"></a> The Report Data Pane  
 No painel de dados do relatório, é possível definir os dados e os recursos de relatório de que você precisa para um relatório antes de criar o layout do relatório. Por exemplo, é possível adicionar fontes de dados, conjuntos de dados, campos calculados, parâmetros de relatório e imagens ao painel de dados do relatório.  
  
 Depois de adicionar itens ao painel de dados do relatório, basta arrastar campos para os itens do relatório na superfície de design para controlar onde os dados são exibidos no relatório.  
  
 Também é possível arrastar campos internos do painel de dados do relatório para a superfície de design do relatório. Quando renderizados, esses campos fornecem informações sobre o relatório, como o nome do relatório, o número total de páginas no relatório e o número da página atual.  
  
 Algumas coisas são adicionadas automaticamente ao painel de dados do relatório quando você adiciona algo à superfície de design de relatório. Por exemplo, se você adicionar uma parte de relatório da Galeria de Partes de Relatório e a parte de relatório for uma região de dados, o conjunto de dados será adicionado automaticamente ao painel de dados do relatório. Para obter mais informações, consulte [Partes de relatório e conjuntos de dados no Construtor de Relatórios](../report-data/report-parts-and-datasets-in-report-builder.md). Além disso, se você inserir uma imagem no relatório, ela será adicionada à pasta Imagens no painel de dados do relatório.  
  
> [!NOTE]  
>  Use o botão **Novo** para adicionar um novo item ao painel de dados do relatório. Você pode adicionar vários conjuntos de dados da mesma fonte de dados ou de outras fontes de dados ao relatório. Você pode adicionar conjuntos de dados compartilhados do servidor de relatório. Para adicionar um novo conjunto de dados da mesma fonte de dados, clique com o botão direito do mouse em uma fonte de dados e clique em **Adicionar Conjunto de Dados**.  
  
 Para obter mais informações sobre itens no painel de dados do relatório, consulte os seguintes tópicos:  
  
-   [Referências globais internas e referências de usuários &#40;relatórios e SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)  
  
-   [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [Imagens &#40;relatórios e SSRS&#41;](../report-design/images-report-builder-and-ssrs.md)  
  
-   [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
-   [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
-   [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
##  <a name="ReptPartGallery"></a> A Galeria de Partes de Relatório  
 A forma mais fácil de criar um relatório é localizando uma parte de relatório existente, como uma tabela ou um gráfico, no servidor de relatório ou em um servidor de relatório integrado a um site do SharePoint. Você procura partes de relatório a serem adicionadas ao relatório na Galeria de Partes de Relatório. É possível filtrar as partes de relatório por todo ou parte do nome da parte de relatório, quem criou, quem modificou por último, quando foi a última modificação, onde está armazenado ou que tipo de parte de relatório. Por exemplo, você pode procurar todos os gráficos criados na semana passada por um de seus colaboradores.  
  
> [!NOTE]  
>  Você deve estar conectado a um servidor para exibir a Galeria de Partes de Relatório.  
  
 Você pode exibir os resultados da pesquisa como miniaturas ou como uma lista, e classificar os resultados da pesquisa por nome, data de criação e modificação, e criador. Para obter mais informações, consulte [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
  
##  <a name="PropertiesPane"></a> O painel Propriedades (Construtor de Relatórios)  
 Todos os itens de um relatório, incluindo seu próprio corpo, regiões de dados, imagens e caixas de texto, possuem propriedades associadas a eles. Por exemplo, a propriedade BorderColor de uma caixa de texto mostra o valor de cor da borda da caixa de texto e PageSize de um relatório indica o tamanho da página do relatório.  
  
 Essas propriedades são exibidas no painel Propriedades. As propriedades no painel mudam de acordo com o item de relatório selecionado.  
  
 Para ver o painel Propriedades, na guia Exibir, no grupo Mostrar/Ocultar, clique em Propriedades.  
  
### <a name="changing-property-values"></a>Alterando os valores das propriedades  
 No Construtor de Relatórios, há várias formas de alterar as propriedades dos itens de relatório:  
  
-   Clicando nos botões e listas da Faixa de Opções.  
  
-   Alterando as configurações das caixas de diálogo.  
  
-   Alterando os valores das propriedades no painel Propriedades.  
  
 As propriedades mais utilizadas estão disponíveis em caixas de diálogo e na Faixa de Opções.  
  
 Dependendo da propriedade, você pode definir um valor de propriedade usando uma lista suspensa, digitando o valor ou clicando em `<Expression>` para criar uma expressão.  
  
### <a name="changing-the-properties-pane-view"></a>Alterando a exibição do painel Propriedades  
 Por padrão, as propriedades exibidas no painel Propriedades são organizadas em grandes categorias, como Ação, Borda, Preenchimento, Fonte e Geral. Cada categoria tem um conjunto de propriedades padrão associado a ela. Por exemplo, as seguintes propriedades são listadas na categoria Fonte: Color, FontFamily, FontSize, FontStyle, FontWeight, LineHeight e TextDecoration. Se preferir, você poderá ordenar todas as propriedades por nome no painel. Isso removerá as categorias e listará todas as propriedades em ordem alfabética, independentemente da categoria.  
  
 Existem três botões na parte superior do painel Propriedades: Categoria, Ordem Alfabética e Páginas de Propriedades. Clique nos botões Categoria e Ordem Alfabética para alternar entre as exibições do painel Propriedades. Clique no botão **Páginas de Propriedades** para abrir a caixa de diálogo de propriedades do item de relatório selecionado.  
  
  
##  <a name="GroupPane"></a> O painel Agrupamento (Construtor de Relatórios)  
 Os grupos são usados para organizar seus dados de relatório em uma hierarquia visual e para calcular totais. Você pode exibir grupos de linhas e colunas de uma região de dados na superfície de design e no painel Agrupamento. O painel Agrupamento possui dois painéis: Grupos de Linhas e Grupos de Colunas. Quando você selecionar uma região de dados, o painel Agrupamento exibirá todos os grupos dessa região de dados no formato de uma lista hierárquica: grupos filho aparecem recuados abaixo dos grupos pai.  
  
 ![Painel Agrupamento para grupos de linhas e colunas aninhadas](../media/rs-basictablixdesigngroupingpanedefaultview.gif "Painel Agrupamento para grupos de linhas e colunas aninhadas")  
  
 É possível criar grupos arrastando campos do painel de dados do relatório e os soltando na superfície de design ou no painel Agrupamento. No painel Agrupamento, você pode adicionar grupos pai, adjacente e filho, alterar as propriedades de grupos e excluir grupos.  
  
 O painel Agrupamento é exibido por padrão, mas você pode fechá-lo desmarcando a caixa Painel Agrupamento na guia Exibir. O painel Agrupamento não está disponível para as regiões de dados Gráfico e Medidor.  
  
 Para obter mais informações, consulte [Painel Agrupamento &#40;Construtor de Relatórios e SSRS&#41;](../report-design/grouping-pane-report-builder.md) e [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](../report-design/understanding-groups-report-builder-and-ssrs.md).  
  
  
##  <a name="RunMode"></a> Visualizando o relatório no modo de execução  
 Na exibição de design do relatório, você não está trabalhando com os dados reais, mas com uma representação dos dados indicados pelo nome do campo ou da expressão. Para ver os dados reais exibidos no contexto do relatório criado, você pode executar o relatório para visualizar os dados do banco de dados subjacente exibidos no layout do relatório. Alternar entre os modos de design e de execução do relatório permite ajustar seu design e ver os resultados imediatamente. Para visualizar o relatório, clique em **executados** na **modos de exibição** grupo na faixa de opções.  
  
 Quando você clica em **Execução**, o Construtor de Relatórios conecta-se às fontes de dados de relatório, armazena em cache os dados do computador, combina os dados e o layout e renderiza o relatório no Visualizador de HTML. O relatório pode ser executado com a frequência desejada durante a fase de criação. Quando estiver satisfeito, você poderá salvá-lo no servidor de relatório onde outras pessoas, com as permissões apropriadas, podem exibi-lo.  
  
### <a name="running-a-report-with-parameters"></a>Executando um relatório com parâmetros  
 Quando é processado, o relatório é processado automaticamente. Se o relatório contiver parâmetros, todos os parâmetros devem ter valores padrão para que o relatório possa ser executado automaticamente. Se um parâmetro não tiver um valor padrão ao ser executado, você precisará escolher um valor para o parâmetro e clicar em **Exibir Relatório** na guia Executar. Para obter mais informações, consulte [Report Parameters &#40;Report Builder and Report Designer&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="print-preview"></a>Visualizar Impressão  
 Quando um relatório é visualizado no modo de execução, ele é semelhante a um relatório gerado em HTML. A visualização não é HTML, mas o layout e a paginação do relatório são semelhantes a uma saída em HTML. Você pode alterar a exibição para representar um relatório impresso alternando para o modo Visualizar Impressão. Clique no botão **Visualizar Impressão** na guia **Execução** . O relatório será exibido como se tivesse sido impresso. Essa exibição é semelhante à saída produzida pelas extensões de renderização de Imagem e PDF. Visualizar Impressão não é um arquivo de imagem ou PDF, embora o layout e a paginação do relatório sejam semelhantes à saída desses formatos.  
  
  
## <a name="see-also"></a>Consulte também  
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
