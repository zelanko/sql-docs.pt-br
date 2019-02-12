---
title: 'Tutorial: Adicionar um gráfico de pizza ao relatório (construtor de relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 30966fc1ccc592539e543869aef03f555ca59b2d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020097"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>Tutorial: Adicionar um gráfico de pizza ao relatório (construtor de relatórios)
  Gráficos de pizza e gráficos de rosca exibem dados como uma proporção do todo. Os gráficos de pizza são os mais usados para fazer comparações entre grupos. Gráficos de pizza e de rosca, além dos gráficos de pirâmide e funil, constituem um grupo de gráficos conhecidos como gráficos de forma. Os gráficos de forma não têm nenhum eixo. Quando um campo numérico é solto em um gráfico de forma, o gráfico calcula a porcentagem de cada valor com relação ao total.  
  
 Se houver muitos pontos de dados em um gráfico de pizza, os rótulos dos pontos de dados podem ficar muito cheios para serem lidos. Nesse caso, use um gráfico de linha. Use gráficos de pizza somente depois de ter agregado seus dados em alguns pontos de dados.  
  
 A ilustração a seguir mostra o gráfico de pizza que você criará.  
  
 ![rs_TutorialPieChartConcave](../../2014/tutorials/media/rs-tutorialpiechartconcave.gif "rs_TutorialPieChartConcave")  
  
##  <a name="BackToTop"></a> O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
1.  [Criar um gráfico de pizza do Assistente de gráfico](#Chart)  
  
2.  [Escolha o tipo de gráfico](#ChartType)  
  
3.  [Exibir as porcentagens em cada fatia](#Percentages)  
  
4.  [Combinar pequenas fatias em uma fatia](#CombineSlices)  
  
5.  [Personalizar o efeito de desenho](#DrawingEffect)  
  
6.  [Adicionar um título de relatório](#Title)  
  
7.  [Salvar o relatório](#Save)  
  
> [!NOTE]  
>  Neste tutorial, as etapas do assistente são consolidadas em dois procedimentos. Para obter instruções passo a passo sobre como navegar até um servidor de relatório, adicionar uma fonte de dados e adicionar um conjunto de dados, consulte o primeiro tutorial nesta série: [Tutorial: Criando um relatório de tabela básica &#40;construtor de relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo estimado para concluir este tutorial: 10 minutos  
  
## <a name="requirements"></a>Requisitos  
 Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Chart"></a> 1. Criar um gráfico de pizza no Assistente de gráfico  
 Na caixa de diálogo Guia de Introdução, use o Assistente de Gráfico para criar um conjunto de dados inserido, escolha uma fonte de dados compartilhada e crie um gráfico de pizza.  
  
> [!NOTE]  
>  Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-create-a-new-chart-report"></a>Para criar um novo relatório de gráfico  
  
1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.  
  
     A caixa de diálogo Guia de Introdução é exibida.  
  
    > [!NOTE]  
    >  Se a caixa de diálogo Guia de Introdução não for exibida, no botão Construtor de Relatórios, clique em **Novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Gráfico**.  
  
4.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados**e em **Avançar**.  
  
5.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou procure o servidor de relatório, selecione uma fonte de dados e clique em **Avançar**. Talvez seja necessário inserir um nome de usuário e uma senha.  
  
    > [!NOTE]  
    >  A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Na página **Crie uma Consulta** , clique em **Editar como Texto**.  
  
7.  Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT 'Advanced Digital Camera' AS Product, CAST(254995.21 AS money) AS Sales  
    UNION SELECT 'Slim Digital Camera' AS Product, CAST(164499.04 AS money) AS Sales  
    UNION SELECT 'SLR Digital Camera' AS Product, CAST(782176.79 AS money) AS Sales  
    UNION SELECT 'Lens Adapter' AS Product, CAST(36333.08 AS money) AS Sales  
    UNION SELECT 'Macro Zoom Lens' AS Product, CAST(40199.3 AS money) AS Sales  
    UNION SELECT 'USB Cable' AS Product, CAST(53245.5 AS money) AS Sales  
    UNION SELECT 'Independent Filmmaker Camcorder' AS Product, CAST(452288.0 AS money) AS Sales  
    UNION SELECT 'Full Frame Digital Camera' AS Product, CAST(247250.85 AS money) AS Sales  
    ```  
  
8.  (Opcional) Clique no botão Executar (**!**) para ver os dados em que o gráfico se baseará.  
  
9. Clique em **Avançar**.  
  
##  <a name="ChartType"></a> 2. Escolher o tipo de gráfico  
 Você pode escolher um dos diversos tipos de gráfico predefinidos.  
  
#### <a name="to-add-a-pie-chart"></a>Para adicionar um gráfico de pizza  
  
1.  Sobre o **escolher um tipo de gráfico** , clique em **pizza**e, em seguida, clique em **próxima**. A página **Organizar campos de gráfico** será aberta.  
  
     Na página **Organizar campos de gráfico** , arraste o campo Produto até o painel **Categorias** . Esse painel define o número de fatias do gráfico de pizza. Neste exemplo, haverá oito fatias, uma para cada produto.  
  
2.  Arraste o campo Vendas até o painel **Valores** . Sales representa a quantidade de vendas da subcategoria. O painel **Valores** exibe `[Sum(Sales)]` porque o gráfico exibe a agregação de cada produto.  
  
3.  Clique em **Avançar**.  
  
4.  Sobre o **escolher um estilo** página, no painel Estilos, selecione um estilo.  
  
     Um estilo especifica um estilo de fonte, um conjunto de cores e um estilo de borda. Quando você selecionar um estilo, o painel Visualizar exibirá um exemplo do gráfico com esse estilo.  
  
5.  Clique em **Concluir**.  
  
     O gráfico é adicionado à superfície de design.  
  
6.  Clique no gráfico para exibir suas alças. Arraste o canto inferior direito do gráfico para aumentar o tamanho do gráfico. Observe que o tamanho da superfície de design de relatório aumenta para acomodar o tamanho do gráfico.  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
 O relatório exibe o gráfico de pizza com oito fatias, uma para cada produto. O tamanho de cada fatia representa as vendas desse produto. Três das fatias são bastante finas.  
  
##  <a name="Percentages"></a> 3. Exibir as porcentagens em cada fatia do gráfico  
 Em cada fatia da pizza, é possível exibir uma porcentagem dessa fatia comparada à pizza inteira.  
  
#### <a name="to-display-percentages-in-each-slice-of-the-pie-chart"></a>Para exibir as porcentagens em cada fatia do gráfico de pizza  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com o botão direito do mouse no gráfico de pizza e clique em **Mostrar Rótulos de Dados**. Os rótulos de dados são exibidos no gráfico.  
  
3.  Um rótulo com o botão direito e, em seguida, clique em **propriedades do rótulo de série**.  
  
4.  Em dados do rótulo, na caixa suspensa, selecione **#PERCENT**.  
  
     Para exibir valores como porcentagens, a propriedade UseValueAsLabel deve ser falsa. Se for solicitado que você defina esse valor na caixa de diálogo **Confirmar Ação** , clique em **Sim**.  
  
5.  (Opcional) Para especificar quantas casas decimais o rótulo deve mostrar, digite `#PERCENT{Pn}` onde *n* é o número de casas decimais a serem exibidas. Por exemplo, para não exibir nenhuma casa decimal, digite `#PERCENT{P0}`.  
  
    > [!NOTE]  
    >  O**Formato de Número** na caixa de diálogo **Propriedades do Rótulo de Série** não tem nenhum efeito quando você formata percentuais. Isso formata os rótulos como porcentagens, mas não calcula qual porcentagem do gráfico de pizza cada fatia representa.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
 O relatório exibe a porcentagem do todo para cada fatia da pizza.  
  
##  <a name="CombineSlices"></a> 4. Combinar pequenas fatias em uma fatia  
 Três das fatias do gráfico são bastante pequenas. É possível combinar várias fatias pequenas em uma fatia maior que representa todas elas.  
  
#### <a name="to-combine-any-slices-on-the-pie-chart-smaller-than-5-percent-into-one-slice"></a>Para combinar fatias no gráfico de pizza menores do que 5% em uma fatia  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Sobre o **modo de exibição** guia da **Mostrar/ocultar** grupo, selecione **propriedades**.  
  
3.  Na superfície de design, clique em qualquer fatia do gráfico de pizza. As propriedades da série são exibidas no painel Propriedades.  
  
4.  Na seção **Geral** , expanda o nó **CustomAttributes** .  
  
5.  Defina a propriedade **CollectedStyle** como **SingleSlice**.  
  
6.  Verifique se a propriedade **CollectedThreshold** está definida como 5.  
  
7.  Verifique se a propriedade **CollectedThresholdUsePercent** está definida como **True**.  
  
8.  Na faixa de opções, sobre o **página inicial** , clique em **executar** para visualizar o relatório.  
  
 Na legenda, a categoria "Outro" agora existe. A nova fatia da pizza combina todas as fatias que estavam abaixo de 5% em uma fatia que representa 6% da pizza inteira.  
  
##  <a name="DrawingEffect"></a> 5. Personalizar o efeito de desenho  
 No Assistente de Gráfico, o estilo padrão de um gráfico de pizza é Ocean, que apresenta um efeito de desenho Côncavo. Você poderá alterá-lo depois de executar o assistente.  
  
#### <a name="to-add-a-drawing-effect-to-the-pie-chart"></a>Para adicionar um efeito de desenho ao gráfico de pizza  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Se o painel Propriedades não estiver aberto, na **modo de exibição** guia, selecione **propriedades**.  
  
3.  Clique duas vezes no próprio gráfico de pizza. As propriedades da série do gráfico de pizza são mostradas no painel Propriedades.  
  
4.  No painel Propriedades, expanda o nó **CustomAttributes** .  
  
5.  Defina as **PieDrawingStyle** à **SoftEdge**.  
  
    > [!NOTE]  
    >  Efeitos de desenho e efeitos tridimensionais são opções exclusivas. Se um gráfico tiver aplicados, de efeitos tridimensionais **PieDrawingStyle** não está disponível no painel de propriedades.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
 A ilustração a seguir mostra o gráfico de pizza com o efeito de borda suave.  
  
 ![rs_TutorialPieChartSoftEdge](../../2014/tutorials/media/rs-tutorialpiechartsoftedge.gif "rs_TutorialPieChartSoftEdge")  
  
##  <a name="Title"></a> 6. Adicionar um título de relatório  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas de Câmeras e Filmadoras**, pressione ENTER e digite **Como um Percentual do Total de Vendas**para que fique assim:  
  
     **Vendas de Câmeras e Filmadoras**  
  
     **Como um Percentual do Total de Vendas**  
  
3.  Selecione **vendas de câmeras e filmadoras**e clique no **negrito** botão da **fonte** seção o **início** guia da faixa de opções.  
  
4.  Selecione **como uma porcentagem do Total de vendas**e, na **fonte** seção o **página inicial** guia, defina o tamanho da fonte como **10**.  
  
5.  (Opcional) Talvez seja necessário aumentar a altura da caixa de texto Título para acomodar as duas linhas de texto.  
  
     Esse título aparecerá na parte superior do relatório. Quando não houver nenhum cabeçalho de página definido, os itens na parte superior do corpo do relatório serão equivalentes a um cabeçalho de relatório.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Save"></a> 7. Salvar o relatório  
  
#### <a name="to-save-the-report"></a>Para salvar o relatório  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  No botão Construtor de Relatórios, clique em **Salvar como**.  
  
3.  Em **Nome**, digite **Gráfico de Pizza de Vendas**.  
  
4.  Clique em **Salvar**.  
  
 O relatório é salvo no servidor de relatório.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você concluiu com êxito o tutorial Adicionando um Gráfico de Pizza ao seu Relatório. Para saber mais sobre gráficos, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) e [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
