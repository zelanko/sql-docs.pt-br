---
title: Definindo uma relação muitos-para-muitos | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 7bebb174-148c-4cbb-a285-2f6d536a16d5
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1fee68a19ece5eab139211939602254db4acff77
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-5-3---defining-a-many-to-many-relationship"></a>Lição 5-3-definir uma relação muitos-para-muitos
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Ao definir uma dimensão, cada fato normalmente se une a somente um membro de dimensão, apesar de um único membro de dimensão poder ser associado a vários fatos diferentes. Por exemplo, cada cliente pode ter muitos pedidos, mas cada pedido pertence a somente um cliente. Na terminologia de banco de dados relacional, isso é chamado de *relação um-para-muitos*. Porém, algumas vezes, um único fato pode se unir a vários membros de dimensão. Na terminologia de banco de dados relacional, isso é chamado de *relação muitos-para-muitos*. Por exemplo, um cliente tem vários motivos para efetuar uma compra, e um motivo de compra pode ser associado a várias compras. Uma tabela de junção é usada para definir os motivos de vendas relacionados a cada compra. Uma dimensão Motivo de Vendas formada por tais relações pode ter, então, vários membros relacionados a uma única transação de vendas. As dimensões muitos para muitos expandem o modelo dimensional além do esquema em estrela clássico e oferecem suporte a análises complexas quando as dimensões não estão relacionadas diretamente a uma tabela de fatos.  
  
No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você define uma relação muitos para muitos entre uma dimensão e um grupo de medidas especificando uma tabela de fatos intermediária que se une à tabela de dimensão. Uma tabela de fatos intermediária é unida, por sua vez, à tabela de dimensão intermediária à qual a tabela de fatos é unida. As relações muitos para muitos entre uma tabela de fatos intermediária e ambas as tabelas de dimensão na relação e a dimensão intermediária criam relações muitos para muitos entre membros da dimensão primária e medidas do grupo de medidas especificado pela relação. Para definir uma relação muitos para muitos entre uma dimensão e um grupo de medidas usando um grupo de medidas intermediário, esse grupo de medidas intermediário deve compartilhar uma ou mais dimensões com o grupo de medidas original.  
  
Com uma dimensão muitos para muitos, os valores são somados distintamente, o que significa que eles não se agregam mais de uma vez ao membro Todos.  
  
> [!NOTE]  
> Para oferecer suporte a uma relação da dimensão muitos para muitos, a relação de chave estrangeira-chave primária deve ser definida na exibição da fonte de dados entre todas as tabelas envolvidas. Caso contrário, não será possível selecionar o grupo de medidas intermediário correto ao estabelecer a relação na guia **Uso da Dimensão** do Designer de Cubo.  
  
Para obter mais informações, consulte [Relações de dimensão](../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)e [Definir uma relação muitos-para-muitos e as propriedades da relação muitos-para-muitos](../analysis-services/multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
Nas tarefas deste tópico, você definirá a dimensão Motivos de Vendas e o grupo de medidas Motivos de Vendas, além de uma relação muitos para muitos entre a dimensão Motivos de Vendas e o grupo de medidas Vendas pela Internet usando o grupo de medidas Motivos de Vendas.  
  
## <a name="adding-required-tables-to-the-data-source-view"></a>Adicionando tabelas necessárias à exibição da fonte de dados  
  
1.  Abra o Designer de Exibição da Fonte de Dados para a exibição da fonte de dados do **Adventure Works DW 2012**  
  
2.  Clique com o botão direito do mouse em qualquer lugar do painel **Organizador de Diagramas** , clique em **Novo Diagrama**e especifique **Motivos do Pedido de Vendas pela Internet** como o nome desse novo diagrama.  
  
3.  Arraste a tabela **InternetSales** do painel **Tabelas** para o painel **Diagrama** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar no painel **Diagrama** e clique em **Adicionar/Remover Tabelas**.  
  
5.  Na caixa de diálogo **Adicionar/Remover Tabelas** , adicione as tabelas **DimSalesReason** e **FactInternetSalesReason** à lista **Objetos incluídos** e clique em **OK**.  
  
    Observe que as relações de chave estrangeira-chave primária entre as tabelas envolvidas foram estabelecidas automaticamente porque aquelas relações são definidas no banco de dados relacional subjacente. Se essas relações não foram definidas em um banco de dados relacional subjacente, talvez seja necessário defini-las na exibição da fonte de dados.  
  
6.  No menu **Formatar** , aponte para **Layout Automático**e, em seguida, clique em **Diagrama**.  
  
7.  Na janela Propriedades, altere o valor da propriedade **FriendlyName** da tabela **DimSalesReason** para **SalesReason**. Depois, altere a propriedade **FriendlyName** da tabela **FactInternetSalesReason** para **InternetSalesReason**.  
  
8.  No painel **Tabelas** , expanda **InternetSalesReason (dbo.FactInternetSalesReason)**, clique em **SalesOrderNumber**e examine a propriedade **DataType** desta coluna de dados na janela Propriedades.  
  
    Observe que o tipo de dados da coluna **SalesOrderNumber** é cadeia de caracteres.  
  
9. Revise os tipos de dados das outras colunas na tabela **InternetSalesReason** .  
  
    Observe que os tipos de dados das outras duas colunas nessa tabela são numéricos.  
  
10. No painel **Tabelas** , clique com o botão direito do mouse em **InternetSalesReason (dbo.FactInternetSalesReason)** e clique em **Explorar Dados**.  
  
    Observe que, para cada número de linha dentro de cada pedido, um valor de chave identifica o motivo das vendas para a compra daquele item de linha, como mostra a imagem a seguir:  
  
    ![O valor para identificar o motivo das compras de chave](../analysis-services/media/l5-many-to-many-1.gif "valor para identificar o motivo das compras de chave")  
  
## <a name="defining-the-intermediate-measure-group"></a>Definindo o grupo de medidas intermediário  
  
1.  Alterne para o Designer de Cubo para o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e depois clique na guia **Estrutura do Cubo** .  
  
2.  Clique com o botão direito do mouse em qualquer lugar do painel **Medidas** e clique em **Novo Grupo de Medidas**. Para obter mais informações, consulte [Criar medidas e grupos de medidas em modelos multidimensionais](../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md).  
  
3.  Na caixa de diálogo **Novo Grupo de Medidas** , selecione **InternetSalesReason** na lista **Selecione uma tabela na exibição da fonte de dados** e clique em **OK**.  
  
    Observe que o grupo de medidas **Motivo de Vendas pela Internet** agora é exibido no painel **Medidas** .  
  
4.  Expanda o grupo de medidas **Motivo de Vendas pela Internet** .  
  
    Observe que somente uma única medida está definida para esse novo grupo de medidas, a medida **Contagem de Motivo de Vendas pela Internet** .  
  
5.  Selecione **Contagem de Motivo de Vendas pela Internet** e revise as propriedades dessa medida na janela Propriedades.  
  
    Observe que a propriedade **AggregateFunction** dessa medida é definida como **Contagem** em vez de **Soma**. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]escolher **contagem** porque o tipo de dados é um tipo de dados de cadeia de caracteres. As outras duas colunas da tabela de fatos subjacente não foram selecionadas como medidas porque o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] identificou-as como chaves numéricas em vez de medidas reais. Para obter mais informações, consulte [Definir um comportamento semiaditivo](../analysis-services/multidimensional-models/define-semiadditive-behavior.md).  
  
6.  Na janela Propriedades, altere a propriedade **Visible** da medida **Contagem do Motivo de Vendas pela Internet** para **False**.  
  
    Essa medida só será usada para unir a dimensão Motivo de Vendas que você definirá próxima ao grupo de medidas Vendas pela Internet. Os usuários não navegarão nessa medida diretamente.  
  
    A imagem a seguir mostra as propriedades da medida **Contagem do Motivo de Vendas pela Internet** .  
  
    ![Propriedades de medida de contagem de motivo de vendas pela Internet](../analysis-services/media/l5-many-to-many-2.gif "propriedades para a medida de contagem de motivo de vendas pela Internet")  
  
## <a name="defining-the-many-to-many-dimension"></a>Definindo a dimensão muitos para muitos  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Dimensões**e clique em **Nova Dimensão**.  
  
2.  Na página **Bem-vindo ao Assistente para Dimensões** , clique em **Avançar**.  
  
3.  Na página **Selecionar Método de Criação** , verifique se a opção **Usar uma tabela existente** está selecionada e clique em **Avançar**.  
  
4.  Na página **Especificar Informações sobre a Origem** , verifique se a exibição da fonte de dados do [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012 está selecionada.  
  
5.  Na lista **Tabela principal** , selecione **SalesReason**.  
  
6.  Na lista **Colunas de chave** , verifique se **SalesReasonKey** está listado.  
  
7.  Na lista **Coluna de nome** , selecione **SalesReasonName**.  
  
8.  Clique em **Avançar**.  
  
9. Na página **Selecionar Atributos de Dimensão** , o atributo **Chave do Motivo de Vendas** é selecionado automaticamente, pois se trata de um atributo de chave. Selecione a caixa de seleção ao lado do atributo **Tipo de Motivo do Motivo de Vendas** , altere o nome para **Tipo do Motivo de Vendas**e, em seguida, clique em **Avançar**.  
  
10. Na página **Concluindo o Assistente** , clique em **Concluir** para criar a dimensão Motivo de Vendas.  
  
11. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
12. No painel **Atributos** do Designer de Dimensão da dimensão **Motivo de Vendas** , selecione **Motivo de Vendas Key**e depois altere a propriedade **Name** na janela Propriedades para **Motivo de Vendas**.  
  
13. No painel **Hierarquias** do Designer de Dimensão, crie uma hierarquia de usuário **Motivos de Vendas** que contenha os níveis **Tipo do Motivo de Vendas** e **Motivo de Vendas** , nessa ordem.  
  
14. Na janela Propriedades, defina **Todos os Motivos de Vendas** como o valor da propriedade **AllMemberName** da hierarquia Motivos de Vendas.  
  
15. Defina **Todos os Motivos de Vendas** como o valor da propriedade **AttributeAllMemberName** da dimensão Motivo de Vendas.  
  
16. Para adicionar uma dimensão criada recentemente ao cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como uma dimensão do cubo, alterne para o **Designer de Cubo**. Na guia **Estrutura do Cubo** , clique com o botão direito do mouse no painel **Dimensões** e selecione **Adicionar Dimensão do Cubo**.  
  
17. Na caixa de diálogo **Adicionar Dimensão do Cubo** , selecione **Motivo de Vendas** e então clique em **OK**.  
  
18. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="defining-the-many-to-many-relationship"></a>Definindo a relação muitos para muitos  
  
1.  Alterne para o Designer de Cubo para o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e então clique na guia **Uso da Dimensão** .  
  
    Observe que a dimensão **Motivo de Vendas** tem uma relação regular definida com o grupo de medidas **Motivo de Vendas pela Internet** , mas não tem relação definida com o grupo de medidas **Vendas pela Internet** ou **Vendas do Revendedor** . Observe também que a dimensão **Detalhes do Pedido de Vendas pela Internet** tem uma relação regular definida com a dimensão **Motivo de Vendas pela Internet** que, por sua vez, tem uma **Relação de Fato** com o grupo de medidas **Vendas pela Internet** . Se essa dimensão não existir (ou outra dimensão com uma relação com os grupos de medidas **Motivo de Vendas pela Internet** e **Vendas pela Internet** não existir), você não conseguirá definir a relação muitos-para-muitos.  
  
2.  Clique na célula na interseção do grupo de medidas **Vendas pela Internet** e da dimensão **Motivo de Vendas** e clique no botão Procurar (**...**).  
  
3.  Na caixa de diálogo **Definir Relação** , selecione **Muitos-para-Muitos** na lista **Selecionar tipo de relação** .  
  
    Você tem que definir o grupo de medidas intermediário que conecta a dimensão Motivo de Vendas ao grupo de medidas Vendas pela Internet.  
  
4.  Na lista **Grupo de medidas intermediário** , selecione **Motivo de Vendas pela Internet**.  
  
    A imagem a seguir mostra as alterações na caixa de diálogo **Definir Relação** :  
  
    ![Caixa de diálogo Definir relação](../analysis-services/media/l5-many-to-many-3.gif "caixa de diálogo Definir relação")  
  
5.  Clique em **OK**.  
  
    Observe o ícone muitos para muitos que representa a relação entre a dimensão Motivo de Vendas e o grupo de medidas Vendas pela Internet.  
  
## <a name="browsing-the-cube-and-the-many-to-many-dimension"></a>Navegando no cubo e na dimensão muitos para muitos  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação finalizar com êxito, alterne para a guia **Navegador** do Designer de Cubo para o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e depois clique no botão **Reconectar**.  
  
3.  Adicione a medida **Vendas pela Internet/Valor das Vendas** à área de dados do painel de dados.  
  
4.  Adicione a hierarquia definida pelo usuário **Motivos de Vendas** da dimensão **Motivo de Vendas** à área de linha do painel de dados.  
  
5.  No painel de metadados, expanda **Cliente**, **Local**, **Geografia do Cliente**, **Membros**, **Todos os Clientes**, **Austrália**, clique com o botão direito do mouse em **Queensland**e, por fim, clique em **Adicionar ao Filtro**.  
  
6.  Expanda cada membro do nível **Tipo de Motivo de Vendas** para revisar os valores em dólar que estão associados a cada motivo que um cliente em Queensland citou para a compra de um produto do [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] pela Internet.  
  
    Observe que os totais associados a cada motivo de vendas são maiores do que as vendas totais. Isso acontece porque alguns clientes citaram vários motivos para suas compras.  
  
    A imagem a seguir mostra os painéis **Filtro** e **Dados** do Designer de Cubo:  
  
    ![Painéis de filtro e dados do Designer de cubo](../analysis-services/media/l5-many-to-many-5.gif "painéis filtro e dados do Designer de cubo")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Definir a granularidade da dimensão dentro de um grupo de medidas](../analysis-services/lesson-5-4-defining-dimension-granularity-within-a-measure-group.md)  
  
## <a name="see-also"></a>Consulte também  
[Trabalhar com diagramas em Designer de exibição de fonte de dados & #40; Analysis Services & #41;](../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
[Relações de dimensão](../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
[Definir uma relação muitos-para-muitos e as propriedades da relação muitos-para-muitos](../analysis-services/multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)  
  
  
  
