---
title: 'Tutorial: Adicionar um gráfico de colunas ao relatório (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 723e8fe5f657d3b9eda2d6ab73966830a13a3aac
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099133"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>Tutorial: Adicionar um gráfico de colunas ao relatório (Construtor de Relatórios)
  Um gráfico de coluna exibe uma série como um conjunto de barras verticais agrupadas por categoria. Um gráfico de coluna pode ser útil para:  
  
-   Mostrar alterações de dados em um período de tempo.  
  
-   Comparar o valor relativo de várias séries.  
  
-   Exibir uma média móvel para mostrar tendências.  
  
 A ilustração seguinte mostra o gráfico de coluna que você criará, com uma média móvel.  
  
 ![rs_TutorialColChartFinished](../../2014/tutorials/media/rs-tutorialcolchartfinished.gif "rs_TutorialColChartFinished")  
  
##  <a name="BackToTop"></a> O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
1.  [Criar um gráfico de Assistente de gráfico](#Chart)  
  
2.  [Escolha o tipo de gráfico](#ChartType)  
  
3.  [Formatar e rotular o Eixo Horizontal](#Horizontal)  
  
4.  [Mova a legenda](#Legend)  
  
5.  [Título do gráfico](#ChartTitle)  
  
6.  [Formatar e rotular o Eixo Vertical](#Vertical)  
  
7.  [Adicionar uma média móvel](#Average)  
  
8.  [Adicionar um título de relatório](#Title)  
  
9. [Salvar o relatório](#Save)  
  
> [!NOTE]  
>  Neste tutorial, as etapas do assistente são consolidadas em um procedimento. Confira instruções passo a passo sobre como navegar até um servidor de relatório, como escolher uma fonte de dados e como criar um conjunto de dados no primeiro tutorial desta série: [Tutorial: Ciar um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo estimado para concluir este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Chart"></a> 1. Criar um relatório de gráfico no Assistente de Gráfico  
 Dos **guia de Introdução** caixa de diálogo, use o Assistente de gráfico para criar um conjunto de dados inserido, escolher uma fonte de dados compartilhada e criar um gráfico de colunas.  
  
> [!NOTE]  
>  Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-create-a-new-chart-report"></a>Para criar um novo relatório de gráfico  
  
1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.  
  
     A caixa de diálogo **Guia de Introdução** é exibida.  
  
    > [!NOTE]  
    >  Se o **guia de Introdução** caixa de diálogo não aparece, da **construtor de relatórios** , clique em **New**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Gráfico**.  
  
4.  Na página **Escolher um conjunto de dados**, clique em **Criar um conjunto de dados**e em **Avançar**.  
  
5.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou procure o servidor de relatório, selecione uma fonte de dados e clique em **Avançar**. Talvez seja necessário inserir um nome de usuário e uma senha.  
  
    > [!NOTE]  
    >  A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
7.  Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT CAST('2009-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2009-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2009-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2009-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2009-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2009-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2009-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2009-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2009-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2009-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2009-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2009-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2009-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2009-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2009-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2009-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (Opcional) Clique no botão Executar (**!**) para ver os dados em que o gráfico se baseará.  
  
9. Clique em **Avançar**.  
  
##  <a name="ChartType"></a> 2. Escolher o tipo de gráfico  
 Você pode escolher um dos diversos tipos de gráfico predefinidos.  
  
#### <a name="to-add-a-column-chart"></a>Para adicionar um gráfico de colunas  
  
1.  Na página **Escolher um tipo de gráfico** , o gráfico de colunas é o tipo de gráfico padrão. Clique em **Avançar**.  
  
2.  Na página **Organizar campos de gráfico** , arraste o campo SalesDate até **Categorias**. As categorias são exibidas no eixo horizontal.  
  
3.  Arraste o campo Sales até **Valores**. A caixa **Valores** exibe Sum(Sales) porque a soma do valor total das vendas é agregada para cada data. Os valores são exibidos no eixo vertical.  
  
4.  Clique em **Avançar**.  
  
5.  Sobre o **escolher um estilo** página, na caixa estilos, selecione um estilo.  
  
     Um estilo especifica um estilo de fonte, um conjunto de cores e um estilo de borda. Quando você selecionar um estilo, o painel Visualizar exibirá um exemplo do gráfico com esse estilo.  
  
6.  Clique em **Concluir**.  
  
     O gráfico é adicionado à superfície de design.  
  
7.  Clique no gráfico para exibir suas alças. Arraste o canto inferior direito do gráfico para aumentar o tamanho do gráfico. Observe que o tamanho da superfície de design de relatório aumenta para acomodar o tamanho do gráfico.  
  
8.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Horizontal"></a> 3. Formatar e rotular o eixo horizontal  
 Por padrão, o eixo horizontal exibe valores em um formato geral que é dimensionado para ajustar o tamanho do gráfico automaticamente.  
  
#### <a name="to-format-a-date-on-the-horizontal-axis"></a>Para formatar uma data no eixo horizontal  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com botão direito do eixo horizontal e, em seguida, clique em **propriedades do Eixo Horizontal**.  
  
3.  Clique em **Número**.  
  
4.  Na **categoria**, selecione **data**.  
  
5.  Na caixa **Tipo** , selecione **31 de janeiro de 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Na guia Início, clique em **Executar** para visualizar o relatório.  
  
 A data é exibida no formato selecionado. Observe que o gráfico não rotula cada categoria no eixo horizontal. Por padrão, somente rótulos que se ajustam próximo ao eixo são incluídos.  
  
 É possível personalizar a exibição de rótulo como o giro dos rótulos e a especificação do intervalo.  
  
#### <a name="to-rotate-the-axis-labels-and-change-the-display-interval-along-the-horizontal-axis"></a>Para girar os rótulos do eixo e alterar o intervalo de exibição ao longo do eixo horizontal  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com botão direito no título do eixo horizontal e, em seguida, clique em **Mostrar título do eixo** para remover o título. Como o eixo horizontal exibe datas, o título não é necessário.  
  
3.  Clique com botão direito do eixo horizontal e, em seguida, clique em **propriedades do Eixo Horizontal**.  
  
4.  No **opções de eixo** página sob **intervalo do eixo e intervalo**, tipo **3** para **intervalo**. O gráfico exibirá a cada três datas.  
  
5.  Clique em **Rótulos**.  
  
6.  Na **alterar opções de ajuste automático do rótulo de eixo**, selecione **desabilitar ajuste automático**.  
  
7.  Em **Ângulo de rotação do rótulo**, selecione **-90**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     O texto de exemplo para o eixo horizontal gira 90 graus.  
  
9. Clique em **Executar** para visualizar o relatório.  
  
 No gráfico, os rótulos são girados e o rótulo a cada três datas é mostrado.  
  
##  <a name="Legend"></a> 4. Mover a legenda  
 A legenda é criada automaticamente de categoria e dados de série.  
  
#### <a name="to-move-the-legend-below-the-chart-area-of-a-column-chart"></a>Para mover a legenda abaixo da área de gráfico de um gráfico de colunas  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  A legenda no gráfico com o botão direito e, em seguida, clique em **propriedades da legenda**.  
  
3.  Para **Layout e posição**, selecione uma posição diferente. Por exemplo, defina a posição para a opção da metade inferior.  
  
     Quando a legenda estiver posicionada na parte superior ou inferior de um gráfico, o layout da legenda será alterado de vertical para horizontal. Você pode selecionar um layout diferente na lista suspensa **Layout** .  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (Opcional) Como há somente uma categoria neste tutorial, a legenda não é necessária. Para remover a legenda, a legenda do botão direito do mouse e, em seguida, clique em **Excluir legenda**.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="ChartTitle"></a> 5. Intitular o gráfico  
  
#### <a name="to-change-the-chart-title-above-the-chart-area"></a>Para alterar o título do gráfico acima da área do gráfico  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Selecione as palavras **título do gráfico** na parte superior do gráfico e, em seguida, digite o seguinte texto: **Store totais de ordem de venda**.  
  
3.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Vertical"></a> 6. Formatar e rotular o eixo vertical  
 Por padrão, o eixo vertical exibe valores em um formato geral que é dimensionado para ajustar o tamanho do gráfico automaticamente.  
  
#### <a name="to-format-as-currency-the-numbers-on-the-vertical-axis"></a>Para formatar os números no eixo vertical como moeda  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes nos rótulos no eixo vertical ao longo do gráfico para selecioná-los.  
  
3.  Na faixa de opções, no **Home** guia o **número** , clique no **moeda** botão. Os rótulos do eixo são alterados para mostrar o formato da moeda.  
  
4.  Na faixa de opções, no **Home** guia o **número** , clique no **diminuir Decimal** botão duas vezes, para mostrar o número arredondado para o valor mais próximo.  
  
5.  Clique com botão direito no eixo vertical e clique em **propriedades do Eixo Vertical**.  
  
6.  Clique em **Número**. Observe que **moeda** já está selecionada na **categoria** caixa, e **casas decimais** já **0** (zero).  
  
7.  No **Mostrar valores em** , clique em **milhares**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Clique com botão direito no título do eixo vertical ao longo do lado do gráfico e clique em **propriedades do título do eixo**.  
  
10. Substitua o texto na **texto do título** campo com o seguinte texto: **Total de vendas (em milhares)**. Também é possível especificar várias opções relacionadas ao modo como o título é formatado.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Average"></a> 7. Adicionar uma média móvel  
  
#### <a name="to-add-a-moving-average"></a>Para adicionar uma média móvel  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes no gráfico para exibir o painel **Dados do Gráfico** .  
  
3.  Com o botão direito do **[SUM (Sales)]** campo que está no **valores** área e clique **adicionar série calculada**.  
  
4.  Em **Fórmula**, verifique se a opção **Média móvel** está selecionada.  
  
5.  Em **Definir Parâmetros da Fórmula**, em **Período**, selecione **4**.  
  
6.  Clique em **borda**.  
  
7.  Na **largura da linha**, selecione **3pt**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Clique em **Executar** para visualizar o relatório.  
  
 O gráfico exibe uma linha que mostra a média móvel para o total de vendas por data, a cada quatro datas.  
  
##  <a name="Title"></a> 8. Adicionar um título de relatório  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Na superfície de design, clique em **Clique para adicionar título**.  
  
3.  Tipo de **gráfico de vendas**, pressione ENTER e, em seguida, digite **janeiro a dezembro de 2009**, portanto, ele tem esta aparência:  
  
     **Gráfico de Vendas**  
  
     **Janeiro a dezembro de 2009**  
  
4.  Selecione **gráfico de vendas**e clique no **negrito** botão no **fonte** seção o **início** guia da faixa de opções.  
  
5.  Selecione **janeiro a dezembro de 2009**e, na **fonte** seção o **página inicial** guia, defina o tamanho da fonte como **10**.  
  
6.  (Opcional) Você talvez precise fazer o **título** altura para acomodar as duas linhas de texto pressionando as setas com pontas duplas quando clicar no meio da borda inferior da caixa de texto.  
  
     Esse título aparecerá na parte superior do relatório. Quando não houver nenhum cabeçalho de página definido, os itens na parte superior do corpo do relatório serão equivalentes a um cabeçalho de relatório.  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Save"></a> 9. Salvar o relatório  
  
#### <a name="to-save-the-report"></a>Para salvar o relatório  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  No botão Construtor de Relatórios, clique em **Salvar como**.  
  
3.  Em **Nome**, digite **Gráfico de Colunas do Pedido de Vendas**.  
  
4.  Clique em **Salvar**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você concluiu com êxito o tutorial Adicionando um gráfico de colunas ao seu relatório. Para saber mais sobre gráficos, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) e [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
