---
title: 'Tutorial: Adicionar um gráfico de barras ao relatório (construtor de relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0b21826cb926dbd5f8b0315f490b20850c6ccd23
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041417"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>Tutorial: Adicionar um gráfico de barras ao relatório (construtor de relatórios)
  Um gráfico de barras exibe os dados de categoria horizontalmente. Ele pode ajudar a:  
  
-   Melhorar a legibilidade de nomes de categorias longos.  
  
-   Melhorar a capacidade de compreensão de tempos plotados como valores.  
  
-   Comparar o valor relativo de várias séries.  
  
 A ilustração a seguir mostra o gráfico de barras que você criará, com as vendas em 2008 e 2009 dos cinco principais vendedores, em ordem alfabética.  
  
 ![rs_BarChartTutorial](../../2014/tutorials/media/rs-barcharttutorial.gif "rs_BarChartTutorial")  
  
##  <a name="BackToTop"></a> O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
1.  [Criar um gráfico de Assistente de gráfico](#Chart)  
  
2.  [Escolha o tipo de gráfico](#ChartType)  
  
3.  [Exibir todos os valores de categoria no eixo Vertical](#AllValues)  
  
4.  [Modificar a exibição de nomes no eixo Vertical](#Sort)  
  
5.  [Mova a legenda](#Legend)  
  
6.  [Mover o título do gráfico](#ChartTitle)  
  
7.  [Formatar e rotular o Eixo Horizontal](#Horizontal)  
  
8.  [Adicionar um filtro para exibir os cinco valores principais](#Filter)  
  
9. [Adicionar um título de relatório](#Title)  
  
10. [Salvar o relatório](#Save)  
  
> [!NOTE]  
>  Neste tutorial, as etapas do assistente são consolidadas em um procedimento. Para obter instruções passo a passo sobre como navegar até um servidor de relatório, criar um conjunto de dados e escolha uma fonte de dados, consulte o primeiro tutorial nesta série: [Tutorial: Criando um relatório de tabela básica &#40;construtor de relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo estimado para concluir este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Chart"></a> 1. Criar um relatório de gráfico no Assistente de Gráfico  
 Dos **guia de Introdução** caixa de diálogo, criar um conjunto de dados inserido, escolher uma fonte de dados compartilhada e criar um gráfico de barras usando o Assistente de gráfico.  
  
> [!NOTE]  
>  Neste tutorial, como contém os valores de dados, a consulta não precisa de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-create-a-new-chart-report"></a>Para criar um novo relatório de gráfico  
  
1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.  
  
     A caixa de diálogo **Guia de Introdução** é exibida.  
  
    > [!NOTE]  
    >  Se o **guia de Introdução** caixa de diálogo não aparecer, clique no botão Construtor de relatórios e, em seguida, clique em **New**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Gráfico**.  
  
4.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados**e em **Avançar**.  
  
5.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou procure o servidor de relatório, selecione uma fonte de dados e clique em **Avançar**. Talvez seja necessário inserir um nome de usuário e uma senha.  
  
    > [!NOTE]  
    >  A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
7.  Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2009, CAST(150000. AS money) AS SalesYear2008  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(190000. AS money) AS SalesYear2008  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2009, CAST(195000. AS money) AS SalesYear2008  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(160000. AS money) AS SalesYear2008  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(220000. AS money) AS SalesYear2008  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(215000. AS money) AS SalesYear2008  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2009, CAST(207000. AS money) AS SalesYear2008  
    ```  
  
8.  (Opcional) Clique no botão Executar (**!**) para ver os dados em que o gráfico se baseará.  
  
9. Clique em **Avançar**.  
  
##  <a name="ChartType"></a> 2. Escolher o tipo de gráfico  
 Você pode escolher um dos diversos tipos de gráfico predefinidos.  
  
#### <a name="to-add-a-column-chart"></a>Para adicionar um gráfico de colunas  
  
1.  Na página **Escolher um tipo de gráfico** , o gráfico de colunas é o tipo de gráfico padrão.  
  
2.  Clique em **Barra**e em **Avançar**.  
  
     Sobre o **organizar campos de gráfico** página, há quatro campos na **campos disponíveis** painel: FirstName, LastName, SalesYear2009 e SalesYear2008.  
  
3.  Arraste LastName para o painel Categorias.  
  
4.  Arraste SalesYear2009 para o painel Valores. SalesYear2009 representa o valor das vendas daquele vendedor no ano de 2009. O painel Valores exibe `[Sum(SalesYear2009)]` porque o gráfico exibe a agregação de cada produto.  
  
5.  Arraste SalesYear2008 para o painel Valores em SalesYear2009. SalesYear2008 representa o valor das vendas daquele vendedor no ano de 2008.  
  
6.  Clique em **Avançar**.  
  
7.  Sobre o **escolher um estilo** página, no painel Estilos, selecione um estilo.  
  
     Um estilo especifica um estilo de fonte, um conjunto de cores e um estilo de borda. Quando você selecionar um estilo, o painel Visualizar exibirá um exemplo do gráfico com esse estilo.  
  
8.  Clique em **Concluir**.  
  
     O gráfico é adicionado à superfície de design.  
  
9. Clique no gráfico para exibir suas alças. Arraste o canto inferior direito do gráfico para aumentar o tamanho do gráfico.  
  
10. Clique em **Executar** para visualizar o relatório.  
  
 O relatório exibe o gráfico de barras para as vendas de cada vendedor nos anos de 2008 e 2009. O comprimento da barra corresponde ao total de vendas.  
  
##  <a name="AllValues"></a> 3. Modificar a exibição de nomes no eixo vertical  
 Por padrão, apenas alguns valores no eixo vertical são exibidos. É possível alterar o gráfico para exibir todas as categorias.  
  
#### <a name="to-display-all-sales-persons-along-the-category-axis-of-a-bar-chart"></a>Para exibir todas as pessoas de vendas junto com o eixo da categoria de um gráfico de barras  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com botão direito no eixo vertical e, em seguida, clique em **propriedades do Eixo Vertical**.  
  
3.  Em **Alcance e intervalo do eixo**, na caixa **Intervalo** , digite **1**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Clique com botão direito vertical **título do eixo** e desmarque as **Mostrar título do eixo** caixa de seleção.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
> [!NOTE]  
>  Se você não conseguir ler os nomes dos vendedores no eixo vertical, poderá aumentar o tamanho do gráfico ou alterar as opções de formatação dos rótulos do eixo.  
  
###  <a name="CategoryExpression"></a> Exibir sobrenome e nome no eixo Vertical  
 Você pode alterar a expressão de categoria para incluir o sobrenome seguido do nome de cada vendedor.  
  
##### <a name="to-change-the-category-expression"></a>Para alterar a expressão de categoria  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes no gráfico para exibir o painel **Dados do Gráfico** .  
  
3.  Na área **Grupos de Categorias** , clique com o botão direito do mouse em [LastName] e clique em **Propriedades do Grupo de Categorias**.  
  
4.  Em Rótulo, clique no botão de expressão (Fx).  
  
5.  Digite a seguinte expressão: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
     Essa expressão concatena o sobrenome, uma vírgula e o nome.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Clique em **Executar** para visualizar o relatório.  
  
 Se os nomes não aparecerem ao executar o relatório, você poderá atualizar os dados manualmente. Enquanto estiver no modo de visualização, na guia **Executar** , no grupo **Navegação** , clique em **Atualizar**.  
  
> [!NOTE]  
>  Se você não conseguir ler os nomes dos vendedores no eixo vertical, poderá aumentar o tamanho do gráfico ou alterar as opções de formatação dos rótulos do eixo.  
  
##  <a name="Sort"></a> 4. Alterar a ordem de classificação de nomes no eixo vertical  
 Quando você classifica dados em um gráfico, está alterando a ordem de valores no eixo de categoria.  
  
#### <a name="to-sort-the-names-in-alphabetical-order-on-the-bar-chart"></a>Para classificar os nomes em ordem alfabética no gráfico de barras  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes no gráfico para exibir o painel **Dados do Gráfico** .  
  
3.  Na área **Grupos de Categorias** , clique com o botão direito do mouse em [LastName] e clique em **Propriedades do Grupo de Categorias**.  
  
4.  Clique em **Classificar**. A página **Alterar opções de classificação** exibe uma lista de expressões de classificação. Por padrão, essa lista contém uma expressão de classificação que é igual à expressão do grupo de categorias original.  
  
5.  Em Classificar por, clique na expressão (**Fx**) botão.  
  
6.  Digite a seguinte expressão: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
7.  Clique em **OK**.  
  
8.  Novamente o **propriedades do grupo de categorias** página, o **ordem** lista suspensa, selecione **Z a**. Isso seleciona ordem alfabética inversa para que os nomes apareçam na ordem de cima para baixo.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Clique em **Executar** para visualizar o relatório.  
  
 Os nomes no eixo horizontal são classificados em ordem inversa, com **Alerca** na parte superior e **Zeng** na parte inferior.  
  
##  <a name="Legend"></a> 5. Mover a legenda  
 Para melhorar a capacidade de leitura dos valores do gráfico, mova a legenda do gráfico. Por exemplo, em um gráfico de barras no qual as barras são mostradas na horizontal, você pode alterar a posição da legenda para que ela fique acima ou abaixo da área do gráfico. Isso dá mais espaço na horizontal às barras.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>Para exibir a legenda abaixo da área de gráfico de um gráfico de barras  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com o botão direito do mouse na legenda no gráfico.  
  
3.  Selecione **Propriedades da Legenda**.  
  
4.  Em **Posição da legenda**, selecione uma posição diferente. Por exemplo, defina a posição para a opção da metade inferior.  
  
     Quando a legenda estiver posicionada na parte superior ou inferior de um gráfico, o layout da legenda será alterado de vertical para horizontal. Você pode selecionar um layout diferente na lista suspensa **Layout** .  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="ChartTitle"></a> 6. Intitular o gráfico  
  
#### <a name="to-change-the-chart-title-above-the-chart-area-of-a-bar-chart"></a>Para alterar o título do gráfico acima da área de gráfico de um gráfico de barras  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Selecione as palavras **título do gráfico** na parte superior do gráfico e, em seguida, digite o seguinte texto: **Vendas para 2008 e 2009**.  
  
3.  Clique em qualquer ponto fora do texto.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Horizontal"></a> 7. Formatar e rotular o eixo horizontal  
 Por padrão, o eixo horizontal exibe valores em um formato geral que é dimensionado para ajustar o tamanho do gráfico automaticamente.  
  
#### <a name="to-format-the-numbers-on-the-horizontal-axis"></a>Para formatar os números no eixo horizontal  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique no eixo horizontal ao longo da parte inferior do gráfico para selecioná-lo.  
  
     Na faixa de opções, no **Home** guia o **número** , clique no **moeda** botão. Os rótulos do eixo horizontal são alterados para moeda.  
  
3.  (Opcional) Remova os dígitos decimais. Próximo ao botão **Moeda** , clique no botão **Diminuir Decimal** duas vezes.  
  
4.  Clique com o botão direito do mouse no eixo horizontal e clique em **Propriedades do Eixo Horizontal**.  
  
5.  Sobre o **número** guia, selecione **Mostrar valores em milhares.**  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Clique com botão direito **título do eixo** e clique em **propriedades do título do eixo**.  
  
8.  No **texto do título** , digite **vendas em milhares** e clique em **Okey**.  
  
9. Clique em **Executar** para visualizar o relatório.  
  
 O relatório exibe a quantidade de vendas no eixo horizontal como moeda em milhares, sem dígitos decimais.  
  
##  <a name="Filter"></a> 8. Adicionar um filtro para exibir os cinco valores principais  
 Você pode adicionar um filtro ao gráfico para especificar os dados do conjunto de dados a serem incluídos ou excluídos no gráfico.  
  
#### <a name="to-add-a-filter-and-display-the-top-five-values"></a>Para adicionar um filtro e exibir os cinco valores principais  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes no gráfico para exibir o painel **Dados do Gráfico** .  
  
3.  Na área **Grupos de Categorias** , clique com o botão direito do mouse no campo [LastName] e clique em **Propriedades do Grupo de Categorias**.  
  
4.  Clique em **Filtros**. A página **Alterar filtros** pode exibir uma lista de expressões de filtro. Por padrão, essa lista está vazia.  
  
5.  Clique em **Adicionar**. Um novo filtro em branco é exibido.  
  
6.  Na **expressão**, digite **[Sum(SalesYear2009)]**. Esse procedimento cria a expressão subjacente `=Sum(Fields!SalesYear2009.Value)`, que poderá ser vista se você clicar no botão **fx** .  
  
7.  Verifique se o tipo de dados é **Text**.  
  
8.  Em **Operador**, selecione **N Superior** na lista suspensa.  
  
9. Em **Valor**, digite a seguinte expressão: **=5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Clique em **Executar** para visualizar o relatório.  
  
 Se os resultados não forem filtrados ao executar o relatório, você poderá atualizar os dados manualmente. Na guia **Executar** do grupo **Navegação** , clique em **Atualizar**.  
  
 O gráfico exibe os cinco nomes de vendedores principais dos dados de vendas de 2009.  
  
##  <a name="Title"></a> 9. Adicionar um título de relatório  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Tipo de **gráfico de barras de vendas**, pressione ENTER e, em seguida, digite **cinco principais vendedores para 2009**, portanto, ele tem esta aparência:  
  
     **Gráfico de Barras de Vendas**  
  
     **Cinco principais vendedores de 2009**  
  
3.  Selecione **Gráfico de Barras de Vendas**e clique no botão **Negrito** .  
  
4.  Selecione **cinco principais vendedores para 2009**e, no **fonte** seção o **página inicial** guia, defina o tamanho da fonte como **10**.  
  
5.  (Opcional) Talvez seja necessário aumentar a altura da caixa de texto Título para acomodar as duas linhas de texto.  
  
     Esse título aparecerá na parte superior do relatório. Quando não houver nenhum cabeçalho de página definido, os itens na parte superior do corpo do relatório serão equivalentes a um cabeçalho de relatório.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Save"></a> 10. Salvar o relatório  
  
#### <a name="to-save-the-report"></a>Para salvar o relatório  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
3.  Em **Nome**, digite **Gráfico de Barras de Vendas**.  
  
4.  Clique em **Salvar**.  
  
 O relatório é salvo no servidor de relatório.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você concluiu com êxito o tutorial Adicionando um gráfico de barras seu relatório. Para saber mais sobre gráficos, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) e [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
