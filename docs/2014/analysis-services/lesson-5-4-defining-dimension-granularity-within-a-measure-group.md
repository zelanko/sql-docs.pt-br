---
title: Definindo a granularidade da dimensão em um grupo de medidas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4f079485-9eb4-405c-9a20-81258298b810
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46d69f2bcc82ba1ff4ae49e9bfa5e3aa7a61ad2a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078457"
---
# <a name="defining-dimension-granularity-within-a-measure-group"></a>Definindo a granularidade da dimensão dentro de um grupo de medidas
  Os usuários podem dimensionar dados de fatos em diferentes granularidades ou especificidades para diversas finalidades. Por exemplo, dados de vendas de revendedores ou pela Internet podem ser gravados diariamente, enquanto que informações sobre cotas de vendas podem ser registradas apenas mensal ou trimestralmente. Nesses cenários, os usuários terão uma dimensão de tempo com granulação ou nível de detalhes diferente para cada uma dessas tabelas de fatos diferentes. Apesar de ser possível definir uma nova dimensão de banco de dados como uma dimensão de tempo com essa granulação diferente, há uma forma mais fácil de fazer isso com o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Por padrão no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], quando uma dimensão é usada dentro de um grupo de medidas, a granulação dos dados dentro daquela dimensão tem como base o atributo de chave da dimensão. Por exemplo, quando uma dimensão de tempo é incluída em um grupo de medidas e a granulação padrão da dimensão de tempo é diária, a granulação padrão dessa dimensão dentro do grupo de medidas é diária. Isso é apropriado em diversas ocasiões, como para os grupos de medidas **Vendas pela Internet** e **Vendas do Revendedor** deste tutorial. Porém, quando tal dimensão é incluída em outros tipos de grupos de medidas, como em um grupo de cotas de vendas ou de medidas de orçamento, uma granulação mensal ou trimestral é geralmente mais apropriada.  
  
 Para especificar uma granulação diferente do padrão para uma dimensão de cubo, você modifica o atributo de granularidade da dimensão do cubo da granularidade usada em determinado grupo de medidas na guia **Uso da Dimensão** do Designer de Cubo. Ao alterar a granulação de uma dimensão dentro de um determinado grupo de medidas para um atributo diferente do atributo de chave daquela dimensão, você deve assegurar que todos os demais atributos do grupo de medidas estejam direta ou indiretamente relacionados ao novo atributo de granularidade. Para isso, você deve especificar relações de atributos entre todos os demais atributos e o atributo que é especificado como atributo de granularidade no grupo de medidas. Nesse caso, você define relações de atributos adicionais em vez de mover relações de atributos. O atributo que é especificado como o atributo de granularidade torna-se efetivamente o atributo de chave dentro do grupo de medidas para os demais atributos da dimensão. Caso as relações de atributo não sejam especificadas apropriadamente, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não conseguirá agregar os valores corretamente, conforme será mostrado nas tarefas deste tópico.  
  
 Para obter mais informações, consulte [Relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)e [Definir uma relação regular e as propriedades da relação regular](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
 Nas tarefas deste tópico, você adicionará um grupo de medidas Cotas de Vendas e definirá a granularidade da dimensão Data nesse grupo de medidas como mensal. Em seguida, você definirá relações de atributos entre o atributo mensal e outros atributos de dimensão para assegurar que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] agregue valores corretamente.  
  
## <a name="adding-tables-and-defining-the-sales-quotas-measure-group"></a>Adicionando tabelas e definindo o grupo de medidas Sales Quotas  
  
1.  Mude para a exibição da fonte de dados **Adventure Works DW 2012** .  
  
2.  Clique com o botão direito do mouse em qualquer lugar no painel **organizador de diagramas** , clique em `Sales Quotas` **novo diagrama**e, em seguida, nomeie o diagrama.  
  
3.  Arraste o **funcionário**, a **região**de vendas `Date` e as tabelas do painel **tabelas** para o painel **diagrama** .  
  
4.  Adicione a tabela **FactSalesQuota** ao painel **Diagrama** clicando com o botão direito do mouse em qualquer lugar do painel **Diagrama** e selecionando **Adicionar/Remover Tabelas**.  
  
     Observe que a tabela **SalesTerritory** é vinculada à tabela **FactSalesQuota** pela tabela **Funcionário** .  
  
5.  Examine as colunas da tabela **FactSalesQuota** e explore os dados dessa tabela.  
  
     Observe que a granulação dos dados dentro dessa tabela é trimestral, que é o nível mais baixo de detalhes na tabela FactSalesQuota.  
  
6.  No designer de exibição da fonte de dados, altere a propriedade **FriendlyName** da tabela `SalesQuotas` **FactSalesQuota** para.  
  
7.  Mude para o cubo Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique na guia **Estrutura do Cubo** .  
  
8.  Clique com o botão direito do mouse em qualquer lugar no painel **medidas** , clique `SalesQuotas` em **novo grupo de medidas**, clique na caixa de diálogo **novo grupo de medidas** e clique em **OK**.  
  
     O `Sales Quotas` grupo de medidas aparece no painel **medidas** . No painel **dimensões** , observe que uma nova `Date` dimensão de cubo também é definida, com base na `Date` dimensão do banco de dados. Uma nova dimensão do cubo relacionada ao tempo é definida porque o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não sabe quais dimensões do cubo relacionadas ao tempo existentes devem ser relacionadas à coluna **DateKey** da tabela de fatos **FactSalesQuota** subjacente ao grupo de medidas Cotas de Vendas. Você alterará isso depois em outra tarefa neste tópico.  
  
9. Expanda `Sales Quotas` o grupo de medidas.  
  
10. No painel **Medidas** , selecione **Cota do Valor de Vendas**e defina o valor da propriedade **FormatString** como **Moeda** na janela Propriedades.  
  
11. Selecione a medida **contagem de cotas de vendas** e, `#,#` em seguida, digite como o valor da propriedade **FormatString** no janela Propriedades.  
  
12. Exclua a medida **trimestre** do calendário `Sales Quotas` do grupo de medidas.  
  
     
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] detectou que a coluna subjacente à medida Trimestre do Calendário contém medidas. Entretanto, essa coluna e a coluna Trimestre Calendário contêm os valores que você utilizará para vincular o grupo de medidas Cotas de Vendas à dimensão Data posteriormente neste tópico.  
  
13. No painel **medidas** , clique com o botão direito `Sales Quotas` do mouse no grupo de medidas e clique em **nova medida**.  
  
     A caixa de diálogo **Nova Medida** é exibida. Essa caixa contém as colunas de origem disponíveis para uma medida com o tipo de uso **Soma**.  
  
14. Na caixa de diálogo **nova medida** , selecione **contagem distinta** na lista **uso** , verifique se `SalesQuotas` está selecionado na lista **tabela de origem** , selecione **EmployeeKey** na lista **coluna de origem** e clique em **OK**.  
  
     Observe que a medida é criada em um novo grupo de medidas chamado **Cotas de Vendas 1**. Medidas de contas distintas no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] são criadas em seus próprios grupos de medidas para maximizar o desempenho de processamento.  
  
15. Altere o valor da propriedade **Name** da medida de **contagem distinta da chave Employee** para `Sales Person Count`e, em seguida `#,#` , digite como o valor para a propriedade **FormatString** .  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>Navegando pelas medidas do grupo de medidas Sales Quota por data  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação for concluída com êxito, clique na guia **Navegador** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique no botão **Reconectar** .  
  
3.  Clique no atalho do Excel e em **Habilitar**.  
  
4.  Na lista de campos da tabela dinâmica, `Sales Quotas` expanda o grupo de medidas e arraste a medida **cota do valor de vendas** até a área valores.  
  
5.  Expanda a dimensão **Sales Territory** e arraste a hierarquia **Sales Territories** definida pelo usuário para Rótulos de Linha.  
  
     Observe que a dimensão do cubo Sales Territory não está relacionada, direta ou indiretamente, à tabela Fact Sales Quota, como mostra a imagem a seguir:  
  
     ![Dimensão do cubo de região de vendas](../../2014/tutorials/media/l5-granularity-2.gif "Dimensão de cubo Região de Vendas")  
  
     Na próxima série de etapas deste tópico, você definirá uma relação de dimensão de referência entre essa dimensão e essa tabela de fatos.  
  
6.  Mova a hierarquia de usuário **Sales Territories** da área Rótulos de Linhas para a área Rótulos de Coluna.  
  
7.  Na lista Campos da Tabela Dinâmica, selecione a hierarquia **Sales Territories** definida pelo usuário e clique na seta para baixo à direita.  
  
     ![A hierarquia Região de Vendas na lista de campos](../../2014/tutorials/media/l5-granularity-1a.png "A hierarquia Região de Vendas na lista de campos")  
  
8.  No filtro, clique na caixa de seleção Selecionar Tudo para desmarcar todas as seleções e escolha somente **América do Norte**.  
  
     ![Painel de filtros para seleção de América do Norte](../../2014/tutorials/media/l5-granularity-1b.png "Painel de filtros para seleção de América do Norte")  
  
9. Na lista de campos da tabela dinâmica `Date`, expanda.  
  
10. Arraste a hierarquia de usuário **Date.Fiscal Date** até Rótulos de Linha  
  
11. Na Tabela Dinâmica, clique na seta para baixo ao lado de Rótulos de Linha. Desmarque todos os anos, com exceção de **FY 2008**.  
  
     Observe que apenas o membro de **julho de 2007** do nível de **mês** é exibido, em vez dos membros de **julho, 2007**, **agosto, 2007**e **setembro, 2007** do nível de **mês** e que apenas o membro 1º de julho `Date` de **2007** do nível é exibido, em vez de todos os 31 dias. Esse comportamento ocorre porque a granulação dos dados na tabela de fatos está no nível trimestre e a granulação da `Date` dimensão é o nível diário. Você alterará esse comportamento na próxima tarefa deste tópico.  
  
     Observe também que o valor **Cota do Valor de Vendas** para os níveis mensal e diário é o mesmo valor do nível trimestral, US$ 13.733.000,00. Isso acontece porque o menor nível de dados no grupo de medidas Cotas de Vendas é o trimestral. Você alterará esse comportamento na Lição 6.  
  
     A imagem a seguir mostra os valores de **Cota do Valor de Vendas**.  
  
     ![Valores para a cota de vendas](../../2014/tutorials/media/l5-granularity-3.png "Valores para a cota de vendas")  
  
## <a name="defining-dimension-usage-properties-for-the-sales-quotas-measure-group"></a>Definindo propriedades de uso de dimensão para o grupo de medidas Sales Quotas  
  
1.  Abra o Designer de Dimensão na dimensão **Funcionário** , clique com o botão direito do mouse em **SalesTerritoryKey** no painel **Exibição da Fonte de Dados** e clique em **Novo Atributo da Coluna**.  
  
2.  No painel **Atributos** , selecione **SalesTerritoryKey**e defina a propriedade **AttributeHierarchyVisible** como **False** na janela Propriedades, a propriedade **AttributeHierarchyOptimizedState** como **NotOptimized**e a propriedade **AttributeHierarchyOrdered** como **False**.  
  
     Esse atributo é necessário para vincular a dimensão **região de vendas** aos `Sales Quotas` grupos de medidas e **cotas de vendas 1** como uma dimensão referenciada.  
  
3.  No designer de cubo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo do tutorial do, clique na guia **uso da dimensão** e examine o uso da dimensão `Sales Quotas` dentro dos grupos de medidas e **cotas de vendas 1** .  
  
     Observe que as **** dimensões de `Date` funcionário e cubo estão vinculadas aos grupos de medidas Sales **Quotasand Sales 1** por meio de relações regulares. Observe também que a dimensão do cubo **Região de Vendas** não está vinculada a nenhum desses grupos de medidas.  
  
4.  Clique na célula na interseção da dimensão **região de vendas** e no `Sales Quotas` grupo de medidas e, em seguida, clique no botão procurar (**...**). A caixa de diálogo **definir relação** é aberta.  
  
5.  Na lista **Selecionar tipo de relação** , selecione **Referenciada**.  
  
6.  Na lista **Dimensão intermediária** , selecione **Funcionário**.  
  
7.  Na lista **Atributo de dimensão de referência** , selecione **Região de Vendas**.  
  
8.  Na lista **Atributo de dimensão intermediária** , selecione **Chave de Região de Vendas**. (A coluna de chave do atributo Região de Vendas é a coluna SalesTerritoryKey.)  
  
9. Verifique se a caixa de seleção **Materializar** está marcada.  
  
10. Clique em **OK**.  
  
11. Clique na célula na interseção da dimensão **região de vendas** e no grupo de medidas **cotas de vendas 1** e, em seguida, clique no botão procurar (**...**). A caixa de diálogo **definir relação** é aberta.  
  
12. Na lista **Selecionar tipo de relação** , selecione **Referenciada**.  
  
13. Na lista **Dimensão intermediária** , selecione **Funcionário**.  
  
14. Na lista **Atributo de dimensão de referência** , selecione **Região de Vendas**.  
  
15. Na lista **Atributo de dimensão intermediária** , selecione **Chave de Região de Vendas**. (A coluna de chave do atributo Região de Vendas é a coluna SalesTerritoryKey.)  
  
16. Verifique se a caixa de seleção **Materializar** está marcada.  
  
17. Clique em **OK**.  
  
18. Exclua `Date` a dimensão do cubo.  
  
     Em vez de ter quatro dimensões de cubo relacionadas ao tempo, você usará a dimensão de cubo Data `Sales Quotas` do **pedido** no grupo de medidas como a data em que as cotas de vendas serão dimensionadas. Você também usará essa dimensão do cubo como a dimensão de data primária no cubo.  
  
19. Na lista **dimensões** , renomeie a dimensão do cubo Data `Date`do **pedido** como.  
  
     Renomear a dimensão do cubo de `Date` data do **pedido** para facilitar para os usuários a compreensão de sua função como a dimensão de data primária neste cubo.  
  
20. Clique no botão procurar (**...**) na célula na interseção do grupo de `Sales Quotas` medidas e da `Date` dimensão.  
  
21. Na caixa de diálogo **Definir Relação** , selecione **Regular** na lista **Selecionar tipo de relação** .  
  
22. Na lista **Atributo de granularidade** , selecione **Calendar Quarter**.  
  
     Observe que um aviso é exibido para notificá-lo de que devido à seleção de um atributo não chave como atributo de granularidade, é necessário certificar-se de que todos os outros atributos estejam, direta ou indiretamente, relacionados ao atributo de granularidade especificando-os como propriedades de membros.  
  
23. Na área **Relação** da caixa de diálogo **Definir Relação** , vincule as colunas de dimensão **CalendarYear** e **CalendarQuarter** da tabela subjacente à dimensão do cubo Date às colunas **CalendarYear** e **CalendarQuarter** na tabela subjacente ao grupo de medidas Sales Quota e clique em **OK**.  
  
    > [!NOTE]  
    >  Calendar Quarter é definido como atributo de granularidade para a dimensão do cubo Data no grupo de medidas Sales Quotas mas o atributo Date continua a ser o atributo de granularidade dos grupos de medidas Internet Sales e Reseller Sales.  
  
24. Repita as quatro etapas anteriores para o grupo de medidas **Sales Quotas 1** .  
  
## <a name="defining-attribute-relationships-between-the-calendar-quarter-attribute-and-the-other-dimension-attributes-in-the-date-dimension"></a>Definindo relações de atributo entre o atributo Calendar Quarter e outros atributos de dimensão na dimensão Date  
  
1.  Alterne para **** o `Date` designer de dimensão da dimensão e, em seguida, clique na guia relações de **atributo** .  
  
     Observe que, embora o **ano civil** esteja vinculado ao **trimestre do calendário** por meio do atributo **semestre do calendário** , os atributos do calendário fiscal são vinculados somente uns aos outros; Eles não estão vinculados ao atributo de **trimestre do calendário** e, portanto, não serão `Sales Quotas` agregados corretamente no grupo de medidas.  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **Trimestre Calendário** e selecione **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Trimestre Calendário**. Defina o **Atributo Relacionado** como **Trimestre Fiscal**.  
  
4.  Clique em **OK**.  
  
     Observe que uma mensagem de aviso é exibida informando que a dimensão contém uma ou mais relações de atributo redundantes que podem impedir que os `Date` dados sejam agregados quando um atributo não chave é usado como um atributo de granularidade.  
  
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
  
     ![Grupo de medidas Cota de Vendas dimensionado corretamente](../../2014/tutorials/media/l5-granularity-7.gif "Grupo de medidas Cota de Vendas dimensionado corretamente")  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 6: Definindo cálculos](lesson-6-defining-calculations.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Definir uma relação regular e propriedades de relação regular](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)   
 [Trabalhar com diagramas no designer de exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
