---
title: Definindo uma relação muitos-para-muitos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7bebb174-148c-4cbb-a285-2f6d536a16d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b7b091c6e963af043533bfe362a801d7d4c91f2
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493872"
---
# <a name="defining-a-many-to-many-relationship"></a>Definindo uma relação muitos-para-muitos
  Quando você define uma dimensão, normalmente cada fato se une a um e apenas um membro de dimensão, enquanto um único membro de dimensão pode ser associado a vários fatos diferentes. Por exemplo, cada cliente pode ter muitos pedidos, mas cada pedido pertence a um único cliente. Na terminologia do banco de dados relacional, isso é chamado de *relação um-para-muitos*. No entanto, às vezes um único fato pode ingressar em vários membros de dimensão. Na terminologia do banco de dados relacional, isso é conhecido como uma *relação muitos-para-muitos*. Por exemplo, um cliente pode ter vários motivos para fazer uma compra, e um motivo de compra pode ser associado a várias compras. Uma tabela de junção é usada para definir os motivos de vendas relacionados a cada compra. Uma dimensão motivo de vendas construída com essas relações teria, então, vários membros relacionados a uma única transação de vendas. Dimensões muitos para muitos expandem o modelo dimensional para além do esquema de estrela clássico e dão suporte à análise complexa quando as dimensões não estão diretamente relacionadas a uma tabela de fatos.  
  
 No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você define uma relação muitos-para-muitos entre uma dimensão e um grupo de medidas especificando uma tabela de fatos intermediária que é unida à tabela de dimensões. Uma tabela de fatos intermediária é unida, por sua vez, a uma tabela de dimensões intermediária para a qual a tabela de fatos está unida. As relações muitos para muitos entre a tabela de fatos intermediária e ambas as tabelas de dimensão na relação e a dimensão intermediária criam as relações muitos para muitos entre os membros da dimensão primária e as medidas na medida grupo especificado pela relação. Para definir uma relação muitos-para-muitos entre uma dimensão e um grupo de medidas por meio de um grupo de medidas intermediário, o grupo de medidas intermediário deve compartilhar uma ou mais dimensões com o grupo de medidas original.  
  
 Com uma dimensão muitos para muitos, os valores são somados distintos, o que significa que eles não agregam mais de uma vez ao membro All.  
  
> [!NOTE]  
>  Para dar suporte a uma relação de dimensão muitos para muitos, uma relação chave primária-chave estrangeira deve ser definida na exibição da fonte de dados entre todas as tabelas envolvidas. Caso contrário, não será possível selecionar o grupo de medidas intermediário correto ao estabelecer a relação na guia **Uso da Dimensão** do Designer de Cubo.  
  
 Para obter mais informações, consulte [relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)e [definir uma relação muitos-para-muitos e propriedades de relação muitos-para-muitos](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
 Nas tarefas deste tópico, você define a dimensão motivos de vendas e o grupo de medidas motivos de vendas, e define uma relação muitos-para-muitos entre a dimensão motivos de vendas e o grupo de medidas Vendas pela Internet por meio do grupo de medidas motivos de vendas.  
  
## <a name="adding-required-tables-to-the-data-source-view"></a>Adicionando tabelas necessárias à exibição da fonte de dados  
  
1.  Abra o designer de exibição da fonte de dados para a exibição da fonte de dados **Adventure Works DW 2012** .  
  
2.  Clique com o botão direito do mouse em qualquer lugar no painel **organizador de diagramas** , clique em **novo diagrama**e especifique `Internet Sales Order Reasons` como o nome desse novo diagrama.  
  
3.  Arraste a tabela **InternetSales** para o painel **diagrama** do painel **tabelas** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar no painel **diagrama** e clique em **Adicionar/remover tabelas**.  
  
5.  Na caixa de diálogo **Adicionar/remover tabelas** , adicione a tabela **DimSalesReason** e a tabela **FactInternetSalesReason** à lista **objetos incluídos** e clique em **OK**.  
  
     Observe que as relações de chave primária-chave estrangeira entre as tabelas envolvidas são estabelecidas automaticamente porque essas relações são definidas no banco de dados relacional subjacente. Se essas relações não tiverem sido definidas no banco de dados relacional subjacente, você precisará defini-las na exibição da fonte.  
  
6.  No menu **Formatar** , aponte para **layout automático**e clique em **diagrama**.  
  
7.  No janela Propriedades, altere a propriedade **FriendlyName** da tabela **DimSalesReason** para `SalesReason` e, em seguida, altere a propriedade **FriendlyName** da tabela **FactInternetSalesReason** para `InternetSalesReason`.  
  
8.  No painel **tabelas** , expanda **InternetSalesReason (dbo. FactInternetSalesReason)** , clique em **SalesOrderNumber**e examine a propriedade **DataType** dessa coluna de dados no janela Propriedades.  
  
     Observe que o tipo de dados da coluna **SalesOrderNumber** é um tipo de dados de cadeia de caracteres.  
  
9. Examine os tipos de dados para as outras colunas na tabela `InternetSalesReason`.  
  
     Observe que os tipos de dados das outras duas colunas nesta tabela são tipos de dados numéricos.  
  
10. No painel **tabelas** , clique com o botão direito do mouse em **InternetSalesReason (dbo. FactInternetSalesReason)** e clique em **explorar dados**.  
  
     Observe que, para cada número de linha dentro de cada pedido, um valor de chave identifica o motivo de vendas para a compra desse item de linha, conforme mostrado na imagem a seguir.  
  
     ![Valor de chave para identificar o motivo de vendas para compras](../../2014/tutorials/media/l5-many-to-many-1.gif "Valor de chave para identificar o motivo de vendas para compras")  
  
## <a name="defining-the-intermediate-measure-group"></a>Definindo o grupo de medidas intermediário  
  
1.  Alterne para o designer de cubo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo de tutorial e clique na guia **estrutura do cubo** .  
  
2.  Clique com o botão direito do mouse em qualquer lugar no painel **medidas** e clique em **novo grupo de medidas**. Para obter mais informações, consulte [criar medidas e grupos de medidas em modelos multidimensionais](multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md).  
  
3.  Na caixa de diálogo **novo grupo de medidas** , selecione `InternetSalesReason` na lista **selecionar uma tabela na exibição da fonte de dados** e clique em **OK**.  
  
     Observe que o grupo de medidas **motivo de vendas pela Internet** agora aparece no painel **medidas** .  
  
4.  Expanda o grupo de medidas **motivo de vendas pela Internet** .  
  
     Observe que apenas uma única medida é definida para esse novo grupo de medidas, a medida **contagem de motivos de vendas pela Internet** .  
  
5.  Selecione **contagem de motivos de vendas pela Internet** e revise as propriedades dessa medida na janela Propriedades.  
  
     Observe que a propriedade **AggregateFunction** dessa medida é definida como **Count** em vez de **sum**. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] escolheu **Count** porque o tipo de dados subjacente é um tipo de dados de cadeia de caracteres. As outras duas colunas na tabela de fatos subjacente não foram selecionadas como medidas porque [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] as detectou como chaves numéricas em vez de medidas reais. Para obter mais informações, consulte [definir o comportamento semiaditivo](multidimensional-models/define-semiadditive-behavior.md).  
  
6.  No janela Propriedades, altere a propriedade **Visible** da medida **contagem de motivos de vendas pela Internet** para **false**.  
  
     Essa medida só será usada para unir a dimensão motivo de vendas que você definirá ao lado do grupo de medidas Vendas pela Internet. Os usuários não irão navegar diretamente nessa medida.  
  
     A imagem a seguir mostra as propriedades da medida **contagem de motivos de vendas pela Internet** .  
  
     ![Propriedades da medida contagem de motivos de vendas pela Internet](../../2014/tutorials/media/l5-many-to-many-2.gif "Propriedades da medida contagem de motivos de vendas pela Internet")  
  
## <a name="defining-the-many-to-many-dimension"></a>Definindo a dimensão muitos para muitos  
  
1.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **dimensões**e clique em **nova dimensão**.  
  
2.  Na página **Bem-vindo ao Assistente para dimensões** , clique em **Avançar**.  
  
3.  Na página **selecionar método de criação** , verifique se a opção **usar uma tabela existente** está selecionada e clique em **Avançar**.  
  
4.  Na página **especificar informações sobre a origem** , verifique se a exibição da fonte de dados [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012 está selecionada.  
  
5.  Na lista **tabela principal** , selecione `SalesReason`.  
  
6.  Na lista **colunas de chave** , verifique se **SalesReasonKey** está listado.  
  
7.  Na lista **coluna de nome** , selecione **SalesReasonName**.  
  
8.  clique em **Avançar**.  
  
9. Na página **Selecionar atributos de dimensão** , o atributo **chave de motivo de vendas** é selecionado automaticamente porque é o atributo de chave. Marque a caixa de seleção ao lado do atributo **tipo de motivo de motivo de vendas** , altere seu nome para `Sales Reason Type` e clique em **Avançar**.  
  
10. Na página **concluindo o assistente** , clique em **concluir** para criar a dimensão motivo de vendas.  
  
11. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
12. No painel **atributos** do designer de dimensão da dimensão **motivo de vendas** , selecione chave de **motivo de vendas**e altere a propriedade **nome** no janela Propriedades para `Sales Reason.`  
  
13. No painel **hierarquias** do designer de dimensão, crie uma hierarquia de usuário **motivos de vendas** que contém o nível de `Sales Reason Type` e o nível de **motivo de vendas** , nessa ordem.  
  
14. Na janela Propriedades, defina `All Sales Reasons` **como o valor para a propriedade** itempropertyname da hierarquia motivos de vendas.  
  
15. Defina `All Sales Reasons` como o valor para a propriedade **AttributeAllMemberName** da dimensão motivo de vendas.  
  
16. Para adicionar uma dimensão criada recentemente ao cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como uma dimensão do cubo, alterne para o **Designer de Cubo**. Na guia **estrutura do cubo** , clique com o botão direito do mouse no painel **dimensões** e selecione **Adicionar dimensão do cubo**.  
  
17. Na caixa de diálogo **Adicionar Dimensão do Cubo** , selecione **Motivo de Vendas** e então clique em **OK**.  
  
18. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="defining-the-many-to-many-relationship"></a>Definindo a relação muitos para muitos  
  
1.  Alterne para o designer de cubo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo de tutorial e clique na guia **uso da dimensão** .  
  
     Observe que a **dimensão motivo de vendas** tem uma relação regular definida com o grupo de medidas motivo de **vendas pela Internet** , mas não tem nenhuma relação definida com os grupos de medidas **vendas pela Internet** ou vendas do **revendedor** . Observe também que a dimensão **Detalhes do Pedido de Vendas pela Internet** tem uma relação regular definida com a dimensão **Motivo de Vendas pela Internet** que, por sua vez, tem uma **Relação de Fato** com o grupo de medidas **Vendas pela Internet** . Se essa dimensão não estiver presente (ou outra dimensão com uma relação com o **motivo de vendas pela Internet** e o grupo de medidas **vendas pela Internet** não estiver presente), você não poderá definir a relação muitos para muitos.  
  
2.  Clique na célula na interseção do grupo de medidas **vendas pela Internet** e na dimensão **motivo de vendas** e, em seguida, clique no botão procurar ( **...** ).  
  
3.  Na caixa de diálogo **definir relação** , selecione **muitos para muitos** na lista **Selecionar tipo de relação** .  
  
     Você tem que definir o grupo de medidas intermediário que conecta a dimensão Motivo de Vendas ao grupo de medidas Vendas pela Internet.  
  
4.  Na lista **grupo de medidas intermediário** , selecione **motivo de vendas pela Internet**.  
  
     A imagem a seguir mostra as alterações na caixa de diálogo **definir relação** .  
  
     ![Caixa de diálogo Definir relação](../../2014/tutorials/media/l5-many-to-many-3.gif "Caixa de diálogo Definir relação")  
  
5.  Clique em **OK**.  
  
     Observe o ícone muitos para muitos que representa a relação entre a dimensão motivo de vendas e o grupo de medidas Vendas pela Internet.  
  
## <a name="browsing-the-cube-and-the-many-to-many-dimension"></a>Navegando no cubo e na dimensão muitos para muitos  
  
1.  No menu **Compilar** , clique em **implantar Analysis Services tutorial**.  
  
2.  Quando a implantação for concluída com êxito, alterne para a guia **navegador** no designer de cubo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo de tutorial e clique em **reconectar**.  
  
3.  Adicione a medida **vendas pela Internet/valor das vendas** à área de dados do painel dados.  
  
4.  Adicione a hierarquia definida pelo usuário **motivos de vendas** da dimensão **motivo de vendas** à área de linha do painel de dados.  
  
5.  No painel de metadados, expanda **cliente**, **local**, **Geografia do cliente**, **Membros**, **todos os clientes**, **Austrália**, clique com o botão direito do mouse em **Queensland**e clique em **Adicionar para filtrar**.  
  
6.  Expanda cada membro do nível de `Sales Reason Type` para revisar os valores de dólar associados a cada motivo pelo qual um cliente do Queensland deu sua compra de um produto de [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] pela Internet.  
  
     Observe que os totais associados a cada motivo de vendas se somam a mais do que o total de vendas. Isso ocorre porque alguns clientes citaram vários motivos para sua compra.  
  
     A imagem a seguir mostra o painel de **filtro** e o painel de **dados** do designer de cubo.  
  
     ![Painéis de filtro e dados do designer de cubo](../../2014/tutorials/media/l5-many-to-many-5.gif "Painéis de filtro e dados do designer de cubo")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa na lição  
 [Definindo a granularidade da dimensão em um grupo de medidas](lesson-5-4-defining-dimension-granularity-within-a-measure-group.md)  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com diagramas &#40;no designer de exibição da fonte de dados Analysis Services&#41; ](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)    
 @No__t_1 de [relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
 [Definir uma relação muitos-para-muitos e propriedades de relação muitos-para-muitos](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)  
  
  
