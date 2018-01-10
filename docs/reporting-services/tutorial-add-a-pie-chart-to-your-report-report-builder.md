---
title: "Tutorial: Adicionar um gráfico de pizza ao relatório (Construtor de Relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
caps.latest.revision: "14"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 68b4e3536833e23be59db3195f5903bfccbc5539
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>Tutorial: Adicionar um gráfico de pizza ao relatório (Construtor de Relatórios)
Neste tutorial, você cria um gráfico de pizza em um relatório paginado do Reporting Services. Você adiciona percentuais e combina fatias pequenas em uma única fatia.

Gráficos de pizza e de rosca exibem dados como uma proporção do todo. Eles não têm eixo. Quando você adiciona um campo numérico a um gráfico de pizza, o gráfico calcula o percentual de cada valor com o total.  

A ilustração a seguir mostra o gráfico de pizza que será criado. 
 
![report-builder-pie-chart-final](../reporting-services/media/report-builder-pie-chart-final.png)
  
Se houver muitos pontos de dados em um gráfico de pizza, os rótulos dos pontos de dados podem ficar muito cheios para serem lidos. Nesse caso, considere a combinação de um número de fatias pequenas em uma fatia maior. Gráficos de pizza são mais fáceis de ler quando você agrega os dados em poucos pontos de dados.  
 
> [!NOTE]  
> Neste tutorial, as etapas do assistente são consolidadas em dois procedimentos. Para obter instruções passo a passo sobre como procurar um servidor de relatório, adicionar uma fonte de dados e um conjunto de dados, consulte o primeiro tutorial desta série: [Tutorial: Criando um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo estimado para concluir este tutorial: 10 minutos  
  
## <a name="requirements"></a>Requisitos  
Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Criar um gráfico de pizza no Assistente de gráfico  
Nesta seção, você usa o Assistente de Gráfico para criar um conjunto de dados inserido, escolhe uma fonte de dados compartilhada e cria um gráfico de pizza.  

  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Gráfico**.  
  
4.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados**e em **Avançar**.  
  
5.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou procure o servidor de relatório, selecione uma fonte de dados e clique em **Avançar**. Talvez seja necessário inserir um nome de usuário e uma senha.  
  
    > [!NOTE]  
    > A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Na página **Crie uma Consulta** , clique em **Editar como Texto**.  
  
7.  Cole a seguinte consulta no painel de consulta:  

    > [!NOTE]  
    > Neste tutorial, a consulta contém os valores de dados e, portanto, ela não precisa de uma fonte de dados externa. Isso torna a consulta longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
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
  
## <a name="ChartType"></a>2. Escolher o tipo de gráfico  
Você pode escolher um dos diversos tipos de gráfico predefinidos.  

  
1.  Na página **Escolher um tipo de gráfico** , clique em **Pizza**e em **Avançar**. A página **Organizar campos de gráfico** será aberta.  
  
    Na página **Organizar campos de gráfico** , arraste o campo Produto até o painel **Categorias** . Esse painel define o número de fatias do gráfico de pizza. Neste exemplo, haverá oito fatias, uma para cada produto.  
  
2.  Arraste o campo Vendas até o painel **Valores** . Sales representa a quantidade de vendas da subcategoria. O painel **Valores** exibe `[Sum(Sales)]` porque o gráfico exibe a agregação de cada produto.  
  
3.  Clique em **Avançar** para ver uma visualização.  
  
5.  Clique em **Concluir**.  
  
    O gráfico é adicionado à superfície de design. Os valores reais do gráfico de pizza não estão visíveis – você vê Produto 1, Produto 2, etc., para dar uma ideia da aparência do gráfico.  
    
    ![report-builder-pie-chart-first-design](../reporting-services/media/report-builder-pie-chart-first-design.png)
  
6.  Clique no gráfico para exibir suas alças. Arraste o canto inferior direito do gráfico para aumentá-lo. Observe que o tamanho da superfície de design do relatório também aumenta para acomodar o tamanho do gráfico.  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
O relatório exibe o gráfico de pizza com oito fatias, uma para cada produto. Agora você verá os produtos reais e o tamanho de cada fatia representa as vendas do produto. Três das fatias são bastante finas.  

![report-builder-pie-chart-first-preview](../reporting-services/media/report-builder-pie-chart-first-preview.png)
  
## <a name="Percentages"></a>3. Exibir as porcentagens em cada fatia do gráfico  
Em cada fatia da pizza, é possível exibir uma porcentagem dessa fatia comparada à pizza inteira.  

  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com o botão direito do mouse no gráfico de pizza e clique em **Mostrar Rótulos de Dados**. Os rótulos de dados são exibidos no gráfico.  
  
3.  Clique com o botão direito do mouse em um rótulo e clique em **Propriedades do Rótulo da Série**.  
  
4.  Na caixa **Rotular dados** , selecione **#PERCENT**.  
    
5.  (Opcional) Para especificar quantas casas decimais o rótulo deve mostrar, na caixa **Rotular dados** após **#PERCENT**, digite **{Pn}** , em que *n* é o número de casas decimais a serem exibidas. Por exemplo, para não exibir nenhuma casa decimal, digite **#PERCENT{P0}**.  

6.  Para exibir valores como porcentagens, a propriedade UseValueAsLabel deve ser falsa. Se for solicitado que você defina esse valor na caixa de diálogo **Confirmar Ação** , clique em **Sim**.  
  
    > [!NOTE]  
    > O**Formato de Número** na caixa de diálogo **Propriedades do Rótulo de Série** não tem nenhum efeito quando você formata percentuais. Isso formata os rótulos como porcentagens, mas não calcula qual porcentagem do gráfico de pizza cada fatia representa.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
O relatório exibe a porcentagem do todo para cada fatia da pizza.  

![report-builder-pie-chart-preview-percents](../reporting-services/media/report-builder-pie-chart-preview-percents.png)
  
## <a name="CombineSlices"></a>4. Combinar pequenas fatias em uma fatia  
Três das fatias do gráfico são bastante pequenas. Você pode combinar várias fatias pequenas em uma maior fatia “Outras” que representa todas elas.  

1.  Alterne para a exibição de design de relatório.  
  
2.  Se o painel Propriedades não estiver visível, na guia **Exibir** > grupo **Mostrar/Ocultar** > selecione **Propriedades**.  
  
3.  Na superfície de design, clique em qualquer fatia do gráfico de pizza. As propriedades da série são exibidas no painel Propriedades.  
  
4.  Na seção **Geral** , expanda o nó **CustomAttributes** .  
  
5.  Defina a propriedade **CollectedStyle** como **SingleSlice**.  

    ![report-builder-pie-chart-single-slice-property](../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
 
6.  Verifique se a propriedade **CollectedThreshold** está definida como 5.  
  
7.  Verifique se a propriedade **CollectedThresholdUsePercent** está definida como **True**.  
  
8.  Na guia **Início** , clique em **Executar** para visualizar o relatório.  
  
Na legenda, agora você vê a categoria “Outros”. A nova fatia da pizza combina todas as fatias que estavam abaixo de 5% em uma fatia que representa 6% da pizza inteira.  

![report-builder-pie-chart-start-at-90](../reporting-services/media/report-builder-pie-chart-start-at-90.png)
 
## <a name="DrawingEffect"></a>5. Iniciar valores do gráfico de pizza na parte superior 

Por padrão, em gráficos de pizza, o primeiro valor do conjunto de dados inicia a 90 graus da parte superior da pizza. Você vê isso no gráfico de pizza nas seções anteriores.

Nesta seção, vamos fazer com que o primeiro valor seja iniciado na parte superior.

1.  Alterne para a exibição de design de relatório.  

2. Clique na própria pizza.

3. No painel Propriedades, em **Atributos Personalizados**, altere PieStartAngle de **0** para **270**.

4. Clique em **Executar** para visualizar o relatório.

Agora, as fatias do gráfico de pizza estão em ordem alfabética, começando na parte superior e terminando na fatia “Outros”.

![report-builder-pie-chart-start-at-top](../reporting-services/media/report-builder-pie-chart-start-at-top.png)
  
## <a name="Title"></a>6. Adicionar um título de relatório  
  
Como o gráfico de pizza é a única visualização do relatório, o gráfico não precisa de seu próprio título. O título do relatório será suficiente.
  
1.  No gráfico, marque a caixa Título do Gráfico e pressione DELETE.

2. Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas de Câmeras e Filmadoras**, pressione ENTER e digite **Como um Percentual do Total de Vendas**para que fique assim:  
  
    **Vendas de Câmeras e Filmadoras**  
  
    **Como um Percentual do Total de Vendas**  
  
3.  Selecione **Vendas de Câmeras e Filmadoras**, na guia **Início** > seção **Fonte** > clique em **Negrito**.  
  
4.  Selecione **Como um Percentual do Total de Vendas** e, na guia **Início** > seção **Fonte**, defina o tamanho da fonte como **10**.  
  
5.  (Opcional) Talvez seja necessário aumentar a altura da caixa de texto Título para acomodar as duas linhas de texto.  
  
    Esse título aparecerá na parte superior do relatório. Quando não houver nenhum cabeçalho de página definido, os itens na parte superior do corpo do relatório serão equivalentes a um cabeçalho de relatório.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="Save"></a>7. Salvar o relatório  
  
### <a name="to-save-the-report"></a>Para salvar o relatório  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  No menu **Arquivo** , clique em **Salvar**.  
  
3.  Em **Nome**, digite **Gráfico de Pizza de Vendas**.  
  
4.  Clique em **Salvar**.  
  
O relatório é salvo no servidor de relatório.  
  
## <a name="next-steps"></a>Next Steps  
Você concluiu com êxito o tutorial Adicionando um Gráfico de Pizza ao seu Relatório. Para saber mais sobre gráficos, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md) e [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
[Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md)  
[Construtor de Relatórios no SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

