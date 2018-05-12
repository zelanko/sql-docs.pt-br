---
title: Definir a granularidade da dimensão dentro de um grupo de medidas | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9faa4c869591c6885a1856fca0ec63661af7799a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-5-4---defining-dimension-granularity-within-a-measure-group"></a>Lição 5-4-Definindo granularidade da dimensão dentro de um grupo de medidas
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Os usuários podem dimensionar dados de fatos em diferentes granularidades ou especificidades para diversas finalidades. Por exemplo, dados de vendas de revendedores ou pela Internet podem ser gravados diariamente, enquanto que informações sobre cotas de vendas podem ser registradas apenas mensal ou trimestralmente. Nesses cenários, os usuários terão uma dimensão de tempo com granulação ou nível de detalhes diferente para cada uma dessas tabelas de fatos diferentes. Apesar de ser possível definir uma nova dimensão de banco de dados como uma dimensão de tempo com essa granulação diferente, há uma forma mais fácil de fazer isso com o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
Por padrão no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], quando uma dimensão é usada dentro de um grupo de medidas, a granulação dos dados dentro daquela dimensão tem como base o atributo de chave da dimensão. Por exemplo, quando uma dimensão de tempo é incluída em um grupo de medidas e a granulação padrão da dimensão de tempo é diária, a granulação padrão dessa dimensão dentro do grupo de medidas é diária. Isso é apropriado em diversas ocasiões, como para os grupos de medidas **Vendas pela Internet** e **Vendas do Revendedor** deste tutorial. Porém, quando tal dimensão é incluída em outros tipos de grupos de medidas, como em um grupo de cotas de vendas ou de medidas de orçamento, uma granulação mensal ou trimestral é geralmente mais apropriada.  
  
Para especificar uma granulação diferente do padrão para uma dimensão de cubo, você modifica o atributo de granularidade da dimensão do cubo da granularidade usada em determinado grupo de medidas na guia **Uso da Dimensão** do Designer de Cubo. Ao alterar a granulação de uma dimensão dentro de um determinado grupo de medidas para um atributo diferente do atributo de chave daquela dimensão, você deve assegurar que todos os demais atributos do grupo de medidas estejam direta ou indiretamente relacionados ao novo atributo de granularidade. Para isso, você deve especificar relações de atributos entre todos os demais atributos e o atributo que é especificado como atributo de granularidade no grupo de medidas. Nesse caso, você define relações de atributos adicionais em vez de mover relações de atributos. O atributo que é especificado como o atributo de granularidade torna-se efetivamente o atributo de chave dentro do grupo de medidas para os demais atributos da dimensão. Caso as relações de atributo não sejam especificadas apropriadamente, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não conseguirá agregar os valores corretamente, conforme será mostrado nas tarefas deste tópico.  
  
Para obter mais informações, consulte [Relações de dimensão](../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)e [Definir uma relação regular e as propriedades da relação regular](../analysis-services/multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
Nas tarefas deste tópico, você adicionará um grupo de medidas Cotas de Vendas e definirá a granularidade da dimensão Data nesse grupo de medidas como mensal. Em seguida, você definirá relações de atributos entre o atributo mensal e outros atributos de dimensão para assegurar que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] agregue valores corretamente.  
  
## <a name="adding-tables-and-defining-the-sales-quotas-measure-group"></a>Adicionando tabelas e definindo o grupo de medidas Sales Quotas  
  
1.  Mude para a exibição da fonte de dados **Adventure Works DW 2012** .  
  
2.  Clique com o botão direito do mouse em qualquer lugar do painel **Organizador de Diagramas** , clique em **Novo Diagrama**e nomeie o diagrama **Sales Quotas**.  
  
3.  Arraste as tabelas **Funcionário**, **Região de Vendas**e **Data** do painel **Tabelas** até o painel **Diagrama** .  
  
4.  Adicione a tabela **FactSalesQuota** ao painel **Diagrama** clicando com o botão direito do mouse em qualquer lugar do painel **Diagrama** e selecionando **Adicionar/Remover Tabelas**.  
  
    Observe que a tabela **SalesTerritory** é vinculada à tabela **FactSalesQuota** pela tabela **Funcionário** .  
  
5.  Examine as colunas da tabela **FactSalesQuota** e explore os dados dessa tabela.  
  
    Observe que a granulação dos dados dentro dessa tabela é trimestral, que é o nível mais baixo de detalhes na tabela FactSalesQuota.  
  
6.  No Designer de Exibição da Fonte de Dados, altere a propriedade **FriendlyName** da tabela **FactSalesQuota** para **SalesQuotas**.  
  
7.  Mude para o cubo Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique na guia **Estrutura do Cubo** .  
  
8.  Clique com o botão direito do mouse em qualquer lugar do painel **Medidas** , clique em **Novo Grupo de Medidas**, em **SalesQuotas** na caixa de diálogo **Novo Grupo de Medidas** e clique em **OK**.  
  
    O grupo de medidas **Cotas de Vendas** é exibido no painel **Medidas** . No painel **Dimensões** , observe que uma nova dimensão do cubo **Data** também está definida com base na dimensão do banco de dados **Data** . Uma nova dimensão do cubo relacionada ao tempo é definida porque o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não sabe quais dimensões do cubo relacionadas ao tempo existentes devem ser relacionadas à coluna **DateKey** da tabela de fatos **FactSalesQuota** subjacente ao grupo de medidas Cotas de Vendas. Você alterará isso depois em outra tarefa neste tópico.  
  
9. Expanda o grupo de medidas **Cotas de Vendas** .  
  
10. No painel **Medidas** , selecione **Cota do Valor de Vendas**e defina o valor da propriedade **FormatString** como **Moeda** na janela Propriedades.  
  
11. Selecione a medida **Contagem das Quotas de Vendas** e digite **#,#** como o valor da propriedade **FormatString** na janela Propriedades.  
  
12. Exclua a medida **Trimestre Calendário** do grupo de medidas **Cotas de Vendas** .  
  
    [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] detectou que a coluna subjacente à medida Trimestre do Calendário contém medidas. Entretanto, essa coluna e a coluna Trimestre Calendário contêm os valores que você utilizará para vincular o grupo de medidas Cotas de Vendas à dimensão Data posteriormente neste tópico.  
  
13. No painel **Medidas** , clique com o botão direito do mouse no grupo de medidas **Cotas de Vendas** e clique em **Nova Medida**.  
  
    A caixa de diálogo **Nova Medida** é exibida. Essa caixa contém as colunas de origem disponíveis para uma medida com o tipo de uso **Soma**.  
  
14. Na caixa de diálogo **Nova Medida** , selecione **Contagem distinta** na lista **Uso** , verifique se **SalesQuotas** está selecionado na lista **Tabela de origem** , selecione **EmployeeKey** na lista **Coluna de origem** e clique em **OK**.  
  
    Observe que a medida é criada em um novo grupo de medidas chamado **Cotas de Vendas 1**. Medidas de contas distintas no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] são criadas em seus próprios grupos de medidas para maximizar o desempenho de processamento.  
  
15. Altere o valor da propriedade **Name** da medida **Conta Distinta da Chave de Funcionário** para **Conta do Vendedor**; em seguida, digite **#,#** como o valor da propriedade **FormatString** .  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>Navegando pelas medidas do grupo de medidas Sales Quota por data  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação for concluída com êxito, clique na guia **Navegador** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique no botão **Reconectar**.  
  
3.  Clique no atalho do Excel e em **Habilitar**.  
  
4.  Na Lista de Campos da Tabela Dinâmica, expanda o grupo de medidas **Sales Quotas** e arraste a medida **Sales Amount Quota** até a área Valores.  
  
5.  Expanda a dimensão **Sales Territory** e arraste a hierarquia **Sales Territories** definida pelo usuário para Rótulos de Linha.  
  
    Observe que a dimensão do cubo Sales Territory não está relacionada, direta ou indiretamente, à tabela Fact Sales Quota, como mostra a imagem a seguir:  
  
    ![Dimensão de cubo região de vendas](../analysis-services/media/l5-granularity-2.gif "dimensão de cubo região de vendas")  
  
    Na próxima série de etapas deste tópico, você definirá uma relação de dimensão de referência entre essa dimensão e essa tabela de fatos.  
  
6.  Mova a hierarquia de usuário **Sales Territories** da área Rótulos de Linhas para a área Rótulos de Coluna.  
  
7.  Na lista Campos da Tabela Dinâmica, selecione a hierarquia **Sales Territories** definida pelo usuário e clique na seta para baixo à direita.  
  
    ![Hierarquia de regiões de vendas na lista de campos](../analysis-services/media/l5-granularity-1a.png "hierarquia região de vendas na lista de campos")  
  
8.  No filtro, clique na caixa de seleção Selecionar Tudo para desmarcar todas as seleções e escolha somente **América do Norte**.  
  
    ![Painel de filtro para selecionar América do Norte](../analysis-services/media/l5-granularity-1b.png "painel de filtro para selecionar América do Norte")  
  
9. Na Lista de Campos da Tabela Dinâmica, expanda **Data**.  
  
10. Arraste a hierarquia de usuário **Date.Fiscal Date** até Rótulos de Linha  
  
11. Na Tabela Dinâmica, clique na seta para baixo ao lado de Rótulos de Linha. Desmarque todos os anos, com exceção de **FY 2008**.  
  
    Observe que somente o membro **July 2007** do nível **Month** é exibido em vez dos membros **July, 2007**, **August, 2007**e **September, 2007** do nível **Month** , e somente o membro **July 1, 2007** do nível **Date** é exibido em vez de todos os 31 dias. Esse comportamento ocorre porque a granulação dos dados na tabela de fatos é trimestral e a granulação da dimensão **Date** é diária. Você alterará esse comportamento na próxima tarefa deste tópico.  
  
    Observe também que o valor **Cota do Valor de Vendas** para os níveis mensal e diário é o mesmo valor do nível trimestral, US$ 13.733.000,00. Isso acontece porque o menor nível de dados no grupo de medidas Cotas de Vendas é o trimestral. Você alterará esse comportamento na Lição 6.  
  
    A imagem a seguir mostra os valores de **Cota do Valor de Vendas**.  
  
    ![Cota do valor de valores de vendas](../analysis-services/media/l5-granularity-3.png "cota do valor de valores de vendas")  
  
## <a name="defining-dimension-usage-properties-for-the-sales-quotas-measure-group"></a>Definindo propriedades de uso de dimensão para o grupo de medidas Sales Quotas  
  
1.  Abra o Designer de Dimensão na dimensão **Funcionário** , clique com o botão direito do mouse em **SalesTerritoryKey** no painel **Exibição da Fonte de Dados** e clique em **Novo Atributo da Coluna**.  
  
2.  No painel **Atributos** , selecione **SalesTerritoryKey**e defina a propriedade **AttributeHierarchyVisible** como **False** na janela Propriedades, a propriedade **AttributeHierarchyOptimizedState** como **NotOptimized**e a propriedade **AttributeHierarchyOrdered** como **False**.  
  
    Esse atributo é necessário para vincular a dimensão **Região de Vendas** aos grupos de medidas **Cotas de Vendas** e **Cotas de Vendas 1** como uma dimensão referenciada.  
  
3.  No Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , clique na guia **Uso da Dimensão** e examine o uso da dimensão nos grupos de medidas **Cotas de Vendas** e **Cotas de Vendas 1** .  
  
    Observe que as dimensões do cubo **Funcionário** e **Data** são vinculadas aos grupos de medidas **Cotas de Vendas e Cotas de Vendas 1** por meio de relações regulares. Observe também que a dimensão do cubo **Região de Vendas** não está vinculada a nenhum desses grupos de medidas.  
  
4.  Clique na célula, na interseção da dimensão **Região de Vendas** e do grupo de medidas **Cotas de Vendas** e clique no botão Procurar (**…**). A caixa de diálogo **Definir Relação** é aberta.  
  
5.  Na lista **Selecionar tipo de relação** , selecione **Referenciada**.  
  
6.  Na lista **Dimensão intermediária** , selecione **Funcionário**.  
  
7.  Na lista **Atributo de dimensão de referência** , selecione **Região de Vendas**.  
  
8.  Na lista **Atributo de dimensão intermediária** , selecione **Chave de Região de Vendas**. (A coluna de chave do atributo Região de Vendas é a coluna SalesTerritoryKey.)  
  
9. Verifique se a caixa de seleção **Materializar** está marcada.  
  
10. Clique em **OK**.  
  
11. Clique na célula, na interseção da dimensão **Região de Vendas** e do grupo de medidas **Cotas de Vendas 1** e clique no botão Procurar (**…**). A caixa de diálogo **Definir Relação** é aberta.  
  
12. Na lista **Selecionar tipo de relação** , selecione **Referenciada**.  
  
13. Na lista **Dimensão intermediária** , selecione **Funcionário**.  
  
14. Na lista **Atributo de dimensão de referência** , selecione **Região de Vendas**.  
  
15. Na lista **Atributo de dimensão intermediária** , selecione **Chave de Região de Vendas**. (A coluna de chave do atributo Região de Vendas é a coluna SalesTerritoryKey.)  
  
16. Verifique se a caixa de seleção **Materializar** está marcada.  
  
17. Clique em **OK**.  
  
18. Exclua a dimensão do cubo **Data** .  
  
    Em vez de ter quatro dimensões do cubo relacionadas ao tempo, você usará a dimensão do cubo **Data do Pedido** no grupo de medidas **Cotas de Vendas** como a data na qual as cotas de vendas serão dimensionadas. Você também usará essa dimensão do cubo como a dimensão de data primária no cubo.  
  
19. Na lista **Dimensões** , renomeie a dimensão do cubo **Order Date** como **Date**.  
  
    Renomear a dimensão do cubo **Order Date** como **Date** faz com que os usuários entendam com mais facilidade que essa é a dimensão de data primária desse cubo.  
  
20. Clique no botão Procurar (**…**) na célula, na intersecção do grupo de medidas **Sales Quotas** e da dimensão **Date** .  
  
21. Na caixa de diálogo **Definir Relação** , selecione **Regular** na lista **Selecionar tipo de relação** .  
  
22. Na lista **Atributo de granularidade** , selecione **Calendar Quarter**.  
  
    Observe que um aviso é exibido para notificá-lo de que devido à seleção de um atributo não chave como atributo de granularidade, é necessário certificar-se de que todos os outros atributos estejam, direta ou indiretamente, relacionados ao atributo de granularidade especificando-os como propriedades de membros.  
  
23. Na área **Relação** da caixa de diálogo **Definir Relação** , vincule as colunas de dimensão **CalendarYear** e **CalendarQuarter** da tabela subjacente à dimensão do cubo Date às colunas **CalendarYear** e **CalendarQuarter** na tabela subjacente ao grupo de medidas Sales Quota e clique em **OK**.  
  
    > [!NOTE]  
    > Calendar Quarter é definido como atributo de granularidade para a dimensão do cubo Data no grupo de medidas Sales Quotas mas o atributo Date continua a ser o atributo de granularidade dos grupos de medidas Internet Sales e Reseller Sales.  
  
24. Repita as quatro etapas anteriores para o grupo de medidas **Sales Quotas 1** .  
  
## <a name="defining-attribute-relationships-between-the-calendar-quarter-attribute-and-the-other-dimension-attributes-in-the-date-dimension"></a>Definindo relações de atributo entre o atributo Calendar Quarter e outros atributos de dimensão na dimensão Date  
  
1.  Mude para o **Designer de Dimensão** da dimensão **Data** e clique na guia **Relações de Atributo** .  
  
    Observe que, apesar de **Ano Calendário** estar vinculado a **Trimestre Calendário** por meio do atributo **Semestre Calendário** , os atributos do calendário fiscal estão vinculados somente uns aos outros; eles não estão vinculados ao atributo **Trimestre Calendário** e, portanto, não serão agregados corretamente no grupo de medidas **Cotas de Vendas** .  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **Trimestre Calendário** e selecione **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Trimestre Calendário**. Defina o **Atributo Relacionado** como **Trimestre Fiscal**.  
  
4.  Clique em **OK**.  
  
    Observe que uma mensagem de aviso é exibida indicando que a dimensão **Date** contém uma ou mais relações de atributo redundantes que podem impedir que os dados sejam agregados quando um atributo não chave é usado como um atributo de granularidade.  
  
5.  Exclua a relação de atributo entre os atributos **Month Name** e **Fiscal Quarter** .  
  
6.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>Navegando pelas medidas do grupo de medidas Sales Quota por data  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação for concluída com êxito, clique na guia **Navegador** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique em **Reconectar**.  
  
3.  Clique no atalho do Excel e em **Habilitar**.  
  
4.  Arraste a medida **Sales Amount Quota** até a área Valores.  
  
5.  Arraste a hierarquia de usuário **Regiões de Vendas** até os Rótulos de Coluna e filtre por **América do Norte**.  
  
6.  Arraste a hierarquia de usuário **Date.FiscalDate** até os Rótulos de Linha; clique na seta para baixo próxima a **Rótulos de Linha** na Tabela Dinâmica e desmarque todas as caixas de seleção que não sejam **FY 2008**para exibir somente o ano fiscal de 2008.  
  
7.  Clique em OK.  
  
8.  Expanda **FY 2008**, **H1 FY 2008**e **Q1 FY 2008**.  
  
    A imagem a seguir mostra uma Tabela Dinâmica para o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] com o grupo de medidas Sales Quota dimensionado corretamente.  
  
    Observe também que todos os membros do nível trimestre fiscal contêm o mesmo valor que o nível trimestral. Usando **Q1 FY 2008** como exemplo, a cota de US$ 9.180.000,00 para **Q1 FY 2008** também é o valor de cada um de seus membros. Isso acontece porque a granulação dos dados na tabela de fatos é trimestral e a granulação da dimensão Date também é trimestral. Na Lição 6, você aprenderá a alocar a quantia trimestral proporcionalmente a cada mês.  
  
    ![Grupo de medidas cota vendas dimensionado corretamente](../analysis-services/media/l5-granularity-7.gif "grupo de medidas cota de vendas dimensionado corretamente")  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 6: Definindo cálculos](../analysis-services/lesson-6-defining-calculations.md)  
  
## <a name="see-also"></a>Consulte também  
[Relações de dimensão](../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
[Definir uma relação regular e as propriedades da relação regular](../analysis-services/multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)  
[Trabalhar com diagramas em um Designer de exibição da fonte de dados &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
  
