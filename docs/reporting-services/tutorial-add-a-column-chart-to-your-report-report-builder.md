---
title: 'Tutorial: Adicionar um gráfico de colunas ao relatório (Construtor de Relatórios) | Microsoft Docs'
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 55a74bcd165fd06d55eccd6afa718ccd775c7faf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041281"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>Tutorial: Adicionar um gráfico de colunas ao relatório (Construtor de Relatórios)
Neste tutorial, você cria um relatório paginado do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] com um gráfico de colunas, exibindo uma série como um conjunto de barras verticais agrupadas por categoria. 

Gráficos de colunas são úteis para:  
  
-   Mostrar alterações de dados em um período de tempo.  
-   Comparar o valor relativo de várias séries.  
-   Exibir uma média móvel para mostrar tendências.  
  
A ilustração seguinte mostra o gráfico de coluna que você criará, com uma média móvel.  
  
![report-builder-column-chart-tutorial](../reporting-services/media/report-builder-column-chart-tutorial.png)    
> [!NOTE]  
> Neste tutorial, as etapas do assistente são consolidadas em um procedimento. Para obter instruções passo a passo sobre como procurar um servidor de relatório, escolher uma fonte de dados e criar um conjunto de dados, consulte o primeiro tutorial desta série: [Tutorial: Criação de um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo estimado para concluir este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Criar um relatório de gráfico no Assistente de Gráfico  
Nesta seção, você aprende a usar o Assistente de Gráfico para criar um conjunto de dados inserido, escolher uma fonte de dados compartilhada e criar um gráfico de colunas.  
  
> [!NOTE]  
> A consulta deste tutorial contém os valores de dados para que ela não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
### <a name="to-create-a-chart-report"></a>Para criar um relatório de gráfico  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Gráfico**.  
  
4.  Na página **Escolher um conjunto de dados**, clique em **Criar um conjunto de dados**e em **Avançar**.  
  
5.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou procure o servidor de relatório, selecione uma fonte de dados e clique em **Avançar**. Talvez seja necessário inserir um nome de usuário e uma senha.  
  
    > [!NOTE]  
    > A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
7.  Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT CAST('2015-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2015-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2015-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2015-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2015-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2015-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2015-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2015-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2015-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2015-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2015-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2015-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2015-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2015-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2015-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2015-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (Opcional) Clique no botão Executar ( **!** ) para ver os dados em que o gráfico se baseará.  
  
9. Clique em **Avançar**.  
  
## <a name="ChartType"></a>2. Escolher o tipo de gráfico  
Você pode escolher um dentre vários tipos de gráficos predefinidos e modificar o gráfico depois de concluir o assistente.  
  
### <a name="to-add-a-column-chart"></a>Para adicionar um gráfico de colunas  
  
1.  Na página **Escolher um tipo de gráfico** , o gráfico de colunas é o tipo de gráfico padrão. Clique em **Avançar**.  
  
2.  Na página **Organizar campos de gráfico** , arraste o campo SalesDate até **Categorias**. As categorias são exibidas no eixo horizontal.  
  
3.  Arraste o campo Sales até **Valores**. A caixa **Valores** exibe Sum(Sales) porque a soma do valor total das vendas é agregada para cada data. Os valores são exibidos no eixo vertical.  
  
4.  Clique em **Avançar**.  
 
6.  Clique em **Concluir**.  
  
    O gráfico é adicionado à superfície de design. Observe que o novo gráfico de colunas mostra apenas dados representacionais. A legenda indica Data de Vendas A, Data de Vendas B, etc., apenas para dar uma ideia da aparência do relatório. 
    
    ![report-builder-column-chart-1-design-view](../reporting-services/media/report-builder-column-chart-1-design-view.png)
  
7.  Clique no gráfico para exibir suas alças. Arraste o canto inferior direito do gráfico para aumentar o tamanho do gráfico. Observe que o tamanho da superfície de design de relatório aumenta para acomodar o tamanho do gráfico.  
  
8.  Clique em **Executar** para visualizar o relatório.  

    ![report-builder-column-chart-1-preview](../reporting-services/media/report-builder-column-chart-1-preview.png)

Observe que o gráfico não rotula cada categoria no eixo horizontal. Por padrão, somente rótulos que se ajustam próximo ao eixo são incluídos. 
  
## <a name="Horizontal"></a>3. Formatar uma data no eixo horizontal  
Por padrão, o eixo horizontal exibe valores em um formato geral que é dimensionado para ajustar o tamanho do gráfico automaticamente.  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com o botão direito do mouse no eixo horizontal > **Propriedades do Eixo Horizontal**.  
  
3.  Na guia **Número** , em **Categoria**, selecione **Data**.  
  
5.  Na caixa **Tipo** , selecione **31 de janeiro de 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Na guia Início, clique em **Executar** para visualizar o relatório.  
  
A data é exibida no formato selecionado. O gráfico ainda não rotula cada categoria no eixo horizontal. 

![report-builder-column-chart-2-preview](../reporting-services/media/report-builder-column-chart-2-preview.png)
  
É possível personalizar a exibição de rótulo como o giro dos rótulos e a especificação do intervalo.  
  
## <a name="4-rotate-the-axis-labels-on-the-horizontal-axis"></a>4. Girar os rótulos de eixo no eixo horizontal  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com o botão direito do mouse no título do eixo horizontal e clique em **Mostrar Título do Eixo** para remover o título. Como o eixo horizontal exibe datas, o título não é necessário.  
  
3.  Clique com o botão direito do mouse no eixo horizontal > **Propriedades do Eixo Horizontal**.  
  
5.  Na guia **Rótulos** , em **Alterar as opções de ajuste automático do rótulo do eixo**, selecione **Desabilitar ajuste automático**.  
  
7.  Em **Ângulo de rotação do rótulo**, selecione **-90**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    O texto de exemplo para o eixo horizontal gira 90 graus.  
    
    ![report-builder-column-chart-rotate-x-axis](../reporting-services/media/report-builder-column-chart-rotate-x-axis.png)
  
9. Clique em **Executar** para visualizar o relatório.  
  
No gráfico, os rótulos são girados.  

![report-builder-column-chart-rotate-x-axis-preview](../reporting-services/media/report-builder-column-chart-rotate-x-axis-preview.png)
  
## <a name="Legend"></a>5. Mover a legenda  
A legenda é criada automaticamente de categoria e dados de série. Você pode mover a legenda abaixo da área de gráfico de um gráfico de colunas.  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com o botão direito do mouse na legenda, no gráfico, > **Propriedades da Legenda**.  
  
3.  Em **Layout e Posição**, selecione uma posição diferente. Por exemplo, selecione a opção intermediária inferior.  
  
    Quando a legenda estiver posicionada na parte superior ou inferior de um gráfico, o layout da legenda será alterado de vertical para horizontal. Você pode selecionar um layout diferente na caixa **Layout** .  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (Opcional) Como há somente uma categoria neste tutorial, o gráfico não precisa de uma legenda. Para removê-la, clique com o botão direito do mouse na legenda > **Excluir Legenda**.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="ChartTitle"></a>6. Intitular o gráfico  
    
1.  Alterne para a exibição de design de relatório.  
  
2.  Selecione as palavras **Título do Gráfico** na parte superior do gráfico e digite **Total de Pedidos de Vendas da Loja**.  
  
3.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="Vertical"></a>7. Formatar e rotular o eixo vertical  
Por padrão, o eixo vertical exibe valores em um formato geral que é dimensionado para ajustar o tamanho do gráfico automaticamente.   
  
1.  Alterne para a exibição de design de relatório.  
  
2. Clique nos rótulos do eixo vertical no lado esquerdo do gráfico para selecioná-los.  
  
3.  Na guia **Início**, no grupo **Número**, clique no botão **Moeda**. Os rótulos do eixo são alterados para mostrar o formato da moeda.  
  
4.  Clique no botão **Diminuir Decimal** duas vezes, para mostrar o número arredondado para o valor mais próximo.  
  
5.  Clique com o botão direito do mouse no eixo vertical > **Propriedades do Eixo Vertical**.  
  
6.  Na guia **Número** , observe que a opção **Moeda** já está selecionada na caixa **Categoria** e **Casas decimais** já é **0** (zero).  
  
7.  Marque **Mostrar Valores em**. **Milhares** já está selecionado.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Clique com o botão direito do mouse no eixo vertical > **Mostrar Título do Eixo**. 

10. Clique com o botão direito do mouse no título do eixo vertical > **Propriedades do Título do Eixo**.  
  
10. Substitua o texto no campo **Texto do título** por **Total de Vendas (em Milhares)** . Também é possível especificar várias opções relacionadas ao modo como o título é formatado.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Clique em **Executar** para visualizar o relatório.  

    ![report-builder-column-chart-format-y-axis](../reporting-services/media/report-builder-column-chart-format-y-axis.png)
    
## <a name="8-show-all-the-labels-on-the-horizontal-x-axis"></a>8. Mostrar todos os rótulos no eixo horizontal (x)

Observe que apenas alguns dos rótulos no eixo x são mostrados. Nesta seção, você define uma propriedade no painel Propriedades para mostrar todas elas.

1.  Alterne para a exibição de design de relatório.  
  
2.  Clique no gráfico e selecione os rótulos do eixo horizontal.

3. No painel Propriedades, defina LabelInterval como 1.

    ![report-builder-column-chart-set-label-interval](../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    O gráfico tem a mesma aparência no modo design. 
    
5.  Clique em **Executar** para visualizar o relatório.

    ![report-builder-column-chart-label-interval-one-preview](../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    Agora o gráfico exibe todos os seus rótulos.
  
## <a name="Average"></a>9. Adicionar uma média móvel com uma série calculada  

Uma média móvel é uma média dos dados na série, calculada ao longo do tempo. A média móvel pode identificar tendências.
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes no gráfico para exibir o painel **Dados do Gráfico** .  
  
3.  Clique com o botão direito do mouse no campo **[Sum(Sales)]** na área **Valores** e clique em **Adicionar Série Calculada**.  

     ![report-builder-column-chart-add-calculated-series](../reporting-services/media/report-builder-column-chart-add-calculated-series.png)
  
4.  Em **Fórmula**, verifique se a opção **Média móvel** está selecionada.  
  
5.  Em **Definir Parâmetros da Fórmula**, em **Período**, selecione **4**.  
  
6.  Na guia **Borda** , em **Largura da linha**, selecione **3pt**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Clique em **Executar** para visualizar o relatório.  
  
O gráfico exibe uma linha que mostra a média móvel para o total de vendas por data, a cada quatro datas. Leia mais sobre como [adicionar uma média móvel a um gráfico](../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md). 

![report-builder-column-chart-moving-average](../reporting-services/media/report-builder-column-chart-moving-average.png)
  
## <a name="Title"></a>10. Adicionar um título de relatório  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Na superfície de design, clique em **Clique para adicionar título**.  
  
3.  Digite **Gráfico de Vendas**, pressione ENTER e digite **Janeiro a dezembro de 2015**, da seguinte forma:  
  
    **Gráfico de Vendas**  
  
    **Janeiro a dezembro de 2015**  
  
4.  Selecione **Gráfico de Vendas** e, na guia **Início**, > seção **Fonte** > **Negrito**.  
  
5.  Selecione **Janeiro a dezembro de 2015** e, na guia **Início**, > seção **Fonte** > defina o tamanho da fonte como **10**.  
  
6.  (Opcional) Talvez seja necessário aumentar a altura da caixa de texto **Título** para acomodar as duas linhas de texto. Mova para baixo as setas com duas pontas ao clicar no meio da borda inferior. Além disso, talvez seja necessário arrastar a parte superior do gráfico para que não haja sobreposição do título.  
  
    Este título é exibido na parte superior do relatório. Quando não houver nenhum cabeçalho de página definido, os itens na parte superior do corpo do relatório serão equivalentes a um cabeçalho de relatório.  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="Save"></a>11. Salvar o relatório  
  
### <a name="to-save-the-report"></a>Para salvar o relatório  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  No botão Construtor de Relatórios, clique em **Salvar como**.  

    Você pode salvá-lo no computador ou no servidor de relatório.
  
3.  Em **Nome**, digite **Gráfico de Colunas do Pedido de Vendas**.  
  
4.  Clique em **Salvar**.  
  
## <a name="next-steps"></a>Next Steps  
Você concluiu com êxito o tutorial Adicionando um gráfico de colunas ao seu relatório. Para saber mais sobre gráficos, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md) e [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
-    [Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md) 
-    [Construtor de Relatórios no SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

