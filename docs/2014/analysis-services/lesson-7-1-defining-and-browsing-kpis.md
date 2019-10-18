---
title: Definindo e navegando por KPIs | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 648b9a02-1278-4f11-b940-6f0de6a4042d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f5d61b3880474851aa0c7302e402ff2f0ac0a47
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493790"
---
# <a name="defining-and-browsing-kpis"></a>Definindo e navegando por KPIs
  Para definir KPIs (indicadores chave de desempenho), primeiro você define um nome de KPI e o grupo de medidas ao qual o KPI está associado. Um KPI pode ser associado a todos os grupos de medidas ou a um único grupo de medidas. Em seguida, você define os seguintes elementos do KPI:  
  
-   A expressão de valor  
  
     Uma expressão de valor é uma medida física, como vendas, uma medida calculada, como lucro, ou um cálculo que é definido dentro do KPI usando uma expressão MDX (Multidimensional Expressions).  
  
-   A expressão de meta  
  
     Uma expressão de meta é um valor ou uma expressão MDX que é resolvida para um valor, que define o destino da medida que a expressão de valor define. Por exemplo, uma expressão de meta pode ser a quantidade pela qual os gerentes de negócios de uma empresa desejam aumentar as vendas ou os lucros.  
  
-   A expressão de status  
  
     Uma expressão de status é uma expressão MDX que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa para avaliar o status atual da expressão de valor em comparação com a expressão de meta. Uma expressão de meta é um valor normalizado no intervalo de-1 a + 1, onde-1 é muito ruim e + 1 é muito bom. A expressão de status exibe um gráfico para ajudá-lo a determinar facilmente o status da expressão de valor em comparação com a expressão de meta.  
  
-   A expressão de tendência  
  
     Uma expressão de tendência é uma expressão MDX que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa para avaliar a tendência atual da expressão de valor em comparação com a expressão de meta. A expressão de tendência ajuda o usuário empresarial a determinar rapidamente se a expressão de valor está se tornando melhor ou pior em relação à expressão de meta. Você pode associar um dos vários gráficos com a expressão de tendência para ajudar os usuários empresariais a entender rapidamente a tendência.  
  
 Além desses elementos que você define para um KPI, você também define várias propriedades de um KPI. Essas propriedades incluem uma pasta de exibição, um KPI pai se o KPI é computado de outros KPIs, o membro da hora atual, se houver, o peso do KPI, se tiver um, e uma descrição do KPI.  
  
> [!NOTE]  
>  Para obter mais exemplos de KPIs, consulte os exemplos de KPI na guia modelos no painel Ferramentas de cálculo ou nos exemplos do data warehouse de exemplo **Adventure Works DW 2012** . Para obter mais informações sobre como instalar esse banco de dados, consulte [install data e Projects de exemplo para o tutorial de modelagem multidimensional Analysis Services](install-sample-data-and-projects.md).  
  
 Na tarefa nesta lição, você definirá KPIs no projeto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tutorial e, em seguida, procurará o cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tutorial usando esses KPIs. Você definirá os seguintes KPIs:  
  
-   Receita do revendedor  
  
     Este KPI é usado para medir como as vendas reais do revendedor se comparam às cotas de vendas para vendas de revendedores, como as vendas são próximas à meta e qual é a tendência de atingir o objetivo.  
  
-   Margem de lucro bruto do produto  
  
     Esse KPI é usado para determinar o quão próximo a margem de lucro bruta é para cada categoria de produto a uma meta especificada para cada categoria de produto e também para determinar a tendência para atingir essa meta.  
  
## <a name="defining-the-reseller-revenue-kpi"></a>Definindo o KPI Receita de revendedor  
  
1.  Abra o designer de cubo para o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo de tutorial e clique na guia **KPIs** .  
  
     A guia **KPIs** inclui vários painéis. No lado esquerdo da guia estão o painel **organizador de KPIs** e o painel **ferramentas de cálculo** . O painel de exibição no meio da guia contém os detalhes do KPI selecionado no painel **organizador de KPIs** .  
  
     A imagem a seguir mostra a guia **KPIs** do designer de cubo.  
  
     ![Guia KPIs do designer de cubo](../../2014/tutorials/media/l7-kpi-1.gif "Guia KPIs do designer de cubo")  
  
2.  Na barra de ferramentas da guia **KPIs** , clique no botão **novo KPI** .  
  
     Um modelo de KPI em branco aparece no painel de exibição, conforme mostrado na imagem a seguir.  
  
     ![Modelo de KPI em branco no painel de exibição](../../2014/tutorials/media/l7-kpi-2.gif "Modelo de KPI em branco no painel de exibição")  
  
3.  Na caixa **nome** , digite `Reseller Revenue` e, em seguida, selecione **vendas do revendedor** na lista **grupo de medidas associado** .  
  
4.  Na guia **metadados** do painel **ferramentas de cálculo** , expanda **medidas**, **vendas do revendedor**e arraste a medida **vendas do revendedor/valor das vendas** até a caixa expressão de **valor** .  
  
5.  Na guia **Metadados** do painel **Ferramentas de Cálculo**, expanda **Medidas** e **Cotas de Vendas** e arraste a medida **Cota do Valor de Vendas** até a caixa **Expressão de Meta**.  
  
6.  Verifique se a opção **Medidor** está selecionada na lista **Indicador de status**. Depois, digite a seguinte expressão MDX na caixa **Expressão de status**:  
  
    ```  
    Case  
     When   
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")>=.95  
       Then 1  
     When  
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")<.95  
       And   
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")>=.85  
       Then 0  
      Else-1  
    End  
    ```  
  
     Essa expressão MDX fornece a base para avaliar o progresso em direção ao objetivo. Nessa expressão MDX, se as vendas reais do revendedor forem mais de 85% da meta, um valor de 0 será usado para preencher o gráfico escolhido. Como um medidor é o gráfico escolhido, o ponteiro no medidor será meio-caminho entre vazio e cheio. Se as vendas reais do revendedor forem mais de 90%, o ponteiro no medidor será de três quartos do caminho entre vazio e cheio.  
  
7.  Verifique se a **seta padrão** está selecionada na lista **indicador de tendência** e digite a seguinte expressão na caixa expressão de **tendência** :  
  
    ```  
    Case  
     When IsEmpty  
      (ParallelPeriod  
       ([Date].[Calendar Date].[Calendar Year],1,  
           [Date].[Calendar Date].CurrentMember))  
      Then 0    
     When  (  
      KpiValue("Reseller Revenue") -   
       (KpiValue("Reseller Revenue"),   
        ParallelPeriod  
         ([Date].[Calendar Date].[Calendar Year],1,  
           [Date].[Calendar Date].CurrentMember))  
          /  
          (KpiValue ("Reseller Revenue"),  
           ParallelPeriod  
            ([Date].[Calendar Date].[Calendar Year],1,  
             [Date].[Calendar Date].CurrentMember)))  
           >=.02  
      Then 1  
       When(  
        KpiValue("Reseller Revenue") -   
         (KpiValue ( "Reseller Revenue" ),  
          ParallelPeriod  
           ([Date].[Calendar Date].[Calendar Year],1,  
            [Date].[Calendar Date].CurrentMember))  
           /  
            (KpiValue("Reseller Revenue"),  
             ParallelPeriod  
              ([Date].[Calendar Date].[Calendar Year],1,  
                [Date].[Calendar Date].CurrentMember)))  
            <=.02  
      Then -1  
       Else 0  
    End  
    ```  
  
     Essa expressão MDX fornece a base para avaliar a tendência em relação à obtenção da meta definida.  
  
## <a name="browsing-the-cube-by-using-the-reseller-revenue-kpi"></a>Navegando no cubo usando o KPI Receita de revendedor  
  
1.  No menu **Compilar** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique em **implantar o tutorial do Analysis Service**.  
  
2.  Quando a implantação for concluída com êxito, na barra de ferramentas da guia **KPIs** , clique no botão **exibição do navegador** e, em seguida, clique em **reconectar**.  
  
     Os medidores de status e tendência são exibidos no painel **navegador KPI** para vendas do revendedor com base nos valores do membro padrão de cada dimensão, junto com o valor do valor e da meta. O membro padrão de cada dimensão é o membro todos do nível todos, porque você não definiu nenhum outro membro de nenhuma dimensão como o membro padrão.  
  
3.  No painel filtro, selecione **território de vendas** na lista **dimensão** , selecione regiões de **vendas** na lista **hierarquia** , selecione **igual** na lista **operador** , marque a caixa de seleção **América do Norte** no Lista de **expressões de filtro** e clique em **OK**.  
  
4.  Na próxima linha do painel de **filtro** , selecione **Data** na lista **dimensão** , selecione data do **calendário** na lista **hierarquia** , selecione **igual** na lista **operador** , marque a caixa de seleção **T3 CY 2007** no Lista de **expressões de filtro** e clique em **OK**.  
  
5.  Clique em qualquer lugar no painel **navegador de KPI** para atualizar os valores do **KPI Receita de revendedor**.  
  
     Observe que as seções **valor**, **meta**e **status** do KPI refletem os valores do novo período de tempo  
  
## <a name="defining-the-product-gross-profit-margin-kpi"></a>Definindo o KPI margem de lucro bruto do produto  
  
1.  Clique no botão **exibição de formulário** na barra de ferramentas da guia **KPIs** e, em seguida, clique no botão **novo KPI** .  
  
2.  Na caixa **nome** , digite `Product Gross Profit Margin` e verifique se **\<All >** aparece na lista **grupo de medidas associado** .  
  
3.  Na guia **metadados** do painel **ferramentas de cálculo** , arraste a medida **total do GPM** para a caixa expressão de **valor** .  
  
4.  Na caixa **expressão de meta** , digite a seguinte expressão:  
  
    ```  
    Case  
        When [Product].[Category].CurrentMember Is  
          [Product].[Category].[Accessories]  
        Then .40                   
        When [Product].[Category].CurrentMember   
          Is [Product].[Category].[Bikes]  
        Then .12                  
        When [Product].[Category].CurrentMember Is  
          [Product].[Category].[Clothing]  
        Then .20  
        When [Product].[Category].CurrentMember Is  
          [Product].[Category].[Components]  
        Then .10  
        Else .12              
    End  
    ```  
  
5.  Na lista **indicador de status** , selecione **cilindro**.  
  
6.  Digite a seguinte expressão MDX na caixa **expressão de status** :  
  
    ```  
    Case  
        When KpiValue( "Product Gross Profit Margin" ) /   
             KpiGoal ( "Product Gross Profit Margin" ) >= .90  
        Then 1  
        When KpiValue( "Product Gross Profit Margin" ) /   
             KpiGoal ( "Product Gross Profit Margin" ) <  .90  
             And   
             KpiValue( "Product Gross Profit Margin" ) /   
             KpiGoal ( "Product Gross Profit Margin" ) >= .80  
        Then 0  
        Else -1  
    End  
    ```  
  
     Essa expressão MDX fornece a base para avaliar o progresso em direção ao objetivo.  
  
7.  Verifique se a **seta padrão** está selecionada na lista **indicador de tendência** e digite a seguinte expressão MDX na caixa expressão de **tendência** :  
  
    ```  
    Case  
    When IsEmpty  
      (ParallelPeriod  
       ([Date].[Calendar Date].[Calendar Year],1,  
           [Date].[Calendar Date].CurrentMember))  
      Then 0    
       When VBA!Abs  
        (  
          KpiValue( "Product Gross Profit Margin" ) -   
           (  
             KpiValue ( "Product Gross Profit Margin" ),  
              ParallelPeriod  
              (   
                [Date].[ Calendar Date].[ Calendar Year],  
                1,  
                [Date].[ Calendar Date].CurrentMember  
              )  
            ) /  
            (  
              KpiValue ( "Product Gross Profit Margin" ),  
              ParallelPeriod  
              (   
                [Date].[ Calendar Date].[ Calendar Year],  
                1,  
                [Date].[ Calendar Date].CurrentMember  
              )  
            )    
          ) <=.02  
      Then 0  
      When KpiValue( "Product Gross Profit Margin" ) -   
           (  
             KpiValue ( "Product Gross Profit Margin" ),  
             ParallelPeriod  
             (   
               [Date].[ Calendar Date].[ Calendar Year],  
               1,  
               [Date].[ Calendar Date].CurrentMember  
             )  
           ) /  
           (  
             KpiValue ( "Product Gross Profit Margin" ),  
             ParallelPeriod  
             (   
               [Date].[Calendar Date].[Calendar Year],  
               1,  
               [Date].[Calendar Date].CurrentMember  
             )  
           )  >.02  
      Then 1  
      Else -1  
    End  
    ```  
  
     Essa expressão MDX fornece a base para avaliar a tendência em relação à obtenção da meta definida.  
  
## <a name="browsing-the-cube-by-using-the-total-gross-profit-margin-kpi"></a>Navegando no cubo usando o KPI de margem de lucro bruto total  
  
1.  No menu **Compilar**, clique em **Implantar Tutorial do Analysis Service**.  
  
2.  Quando a implantação for concluída com êxito, clique no botão **Reconectar** na barra de ferramentas da guia **KPIs** e clique em **Exibição de Navegador**.  
  
     O `Product Gross Profit Margin` KPI é exibido e exibe o valor do KPI para **Q3 CY 2007** e a região de vendas **América do Norte** .  
  
3.  No painel **Filtro**, selecione **Produto** na lista **Dimensão**, **Categoria** na lista **Hierarquia**, **Igual** na lista **Operador**, **Bicicletas** na lista **Expressão de Filtro** e clique em **OK**.  
  
     A margem de lucro bruto da venda de bicicletas por revendedores em América do Norte no T3 CY 2007 é exibida.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 8: definindo ações](lesson-8-defining-actions.md)  
  
  
