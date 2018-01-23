---
title: "Definindo e usando uma ação de detalhamento | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 3765f865-2b93-44be-b290-28e3815d5ecb
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d15da8a4d463cbe2e8b0b05abf163400dc354749
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2018
---
# <a name="lesson-8-1---defining-and-using-a-drillthrough-action"></a>Lição 8-1-Definindo e usando uma ação de detalhamento
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Os dados de fato de dimensionamento em uma dimensão de fatos sem filtrar corretamente os dados que a consulta retorna podem causar lentidão no desempenho da consulta. Para evitar esse problema, defina uma ação de detalhamento que restrinja o número total de linhas que serão retornadas. Esse processo melhorará significativamente o desempenho da consulta.  
  
Nas tarefas deste tópico, você definirá uma ação de detalhamento para retornar informações sobre os detalhes do pedido de vendas para clientes na Internet.  
  
## <a name="defining-the-drillthrough-action-properties"></a>Definindo as propriedades da ação de detalhamento  
  
1.  No Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , clique na guia **Ações** .  
  
    A guia **Ações** inclui vários painéis. No lado esquerdo da guia estão os painéis **Organizador de Ações** e **Ferramentas de Cálculo** . O painel à direita desses dois painéis está o painel **Exibição** , que contém os detalhes da ação selecionada no painel **Organizador de Ações** .  
  
    A imagem a seguir mostra a guia **Ações** do Designer de Cubo.  
  
    ![Guia Ações do Designer de cubo](../analysis-services/media/l8-action1.gif "guia Ações do Designer de cubo")  
  
2.  Na barra de ferramentas da guia **Ações** , clique no botão **Nova Ação de Detalhamento** .  
  
    Um modelo de ação em branco será exibido na tela.  
  
    ![Modelo de ação em branco no painel de exibição](../analysis-services/media/l8-action2.gif "modelo de ação em branco no painel de exibição")  
  
3.  Na caixa **Nome** , altere o nome dessa ação para **Ação de Detalhamento dos Detalhes de Vendas pela Internet**.  
  
4.  Na lista **Membros do grupo de medidas** , selecione **Vendas pela Internet**.  
  
5.  Na caixa **Colunas de Detalhamento** , selecione **Detalhes de Pedidos de Vendas pela Internet** na lista **Dimensões** .  
  
6.  Na lista **Retornar Colunas** , marque as caixas de seleção **Descrição do Item** e **Número do Pedido** e clique em **OK**. A imagem a seguir mostra como o modelo Ação deve estar sendo exibido neste momento no procedimento.  
  
    ![Caixa colunas de detalhamento](../analysis-services/media/l8-action3.gif "caixa colunas de detalhamento")  
  
7.  Expanda a caixa **Propriedades Adicionais** , como mostra a imagem a seguir.  
  
    ![Caixa propriedades adicionais](../analysis-services/media/l8-action4.gif "caixa propriedades adicionais")  
  
8.  Na caixa **Máximo de Linhas** , digite **10**.  
  
9. Na caixa **Legenda** , digite **Detalhamento até Detalhes do Pedido…**.  
  
    Essas configurações limitam o número de linhas a serem retornadas e especificam a legenda que será exibida no menu do aplicativo cliente. A imagem a seguir mostra essas configurações na caixa **Propriedades Adicionais** .  
  
    ![Caixa propriedades adicionais](../analysis-services/media/l8-action5.gif "caixa propriedades adicionais")  
  
## <a name="using-the-drillthrough-action"></a>Usando a ação de detalhamento  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação for concluída com êxito, clique na guia **Navegador** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique no botão **Reconectar** .  
  
3.  Inicie o Excel.  
  
4.  Adicione a medida **Vendas pela Internet/Valor das Vendas** à área Valores.  
  
5.  Adicione a hierarquia definida pelo usuário **Geografia do Cliente** da pasta **Local** na dimensão **Customer** à área **Filtro de Relatório** .  
  
6.  Na Tabela Dinâmica, em **Geografia do Cliente**, adicione um filtro que seleciona um único cliente. Expanda **Todos os clientes**, **Austrália**, **Queensland**, **Brisbane**e **4000**, marque a caixa de seleção **Adam Powell**e clique em **OK**.  
  
    O total de vendas em produtos da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] obtido por Adam Powell será exibido na área de dados.  
  
7.  Clique com o botão direito do mouse no valor de vendas, aponte para **Ações Adicionais**e clique em **Detalhamento até Detalhes do Pedido**.  
  
    Os detalhes dos pedidos que foram enviados a Adam Powell são exibidos no **Visualizador de Exemplos de Dados**, como mostra a imagem a seguir. Entretanto, alguns detalhes adicionais também seriam úteis, como a data do pedido, a data de vencimento e a data de envio. No próximo procedimento, você adicionará esses detalhes.  
  
    ![Pedidos enviados a Adam Powell](../analysis-services/media/l8-action6.gif "pedidos enviados a Adam Powell")  
  
8.  Feche o Excel/  
  
## <a name="modifying-the-drillthrough-action"></a>Modificando a ação de detalhamento  
  
1.  Abra o Designer de Dimensão na dimensão **Detalhes do Pedido de Vendas pela Internet** .  
  
    Observe que apenas três atributos foram definidos para essa dimensão.  
  
2.  No painel **Exibição da Fonte de Dados** , clique com o botão direito do mouse em uma área aberta e clique em **Mostrar Todas as Tabelas**.  
  
3.  No menu **Formatar** , aponte para **Layout Automático** e clique em **Diagrama**.  
  
4.  Localize a tabela **InternetSales (dbo.FactInternetSales)** clicando com o botão direito do mouse em uma área aberta do painel **Exibição da Fonte de Dados** . Em seguida, clique em **Localizar Tabela** , em **InternetSales** e em **OK**.  
  
5.  Crie novos atributos com base nas seguintes colunas:  
  
    -   OrderDateKey  
  
    -   DueDateKey  
  
    -   ShipDateKey  
  
6.  Altere a propriedade **Name** do atributo **Chave de Data do Pedido** para **Data do Pedido** . Em seguida, clique no botão Procurar da propriedade **Name Column** e, na caixa de diálogo **Coluna de Nome** , selecione **Data** como a tabela de origem e SimpleDate como a coluna de origem. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Altere a propriedade **Name** do atributo **Due Date Key** para **Due Date**. Em seguida, usando o mesmo método do atributo **Order Date Key** , altere a propriedade **Name Column** deste atributo para **Date.SimpleDate (WChar)**.  
  
8.  Altere a propriedade **Name** do atributo **Ship Date Key** para **Ship Date**. Em seguida, altere a propriedade **Name Column** deste atributo para **Date.SimpleDate (WChar)**.  
  
9. Mude para a guia **Ações** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
10. Na lista **Colunas de Detalhamento** , marque as caixas de seleção para adicionar as seguintes colunas à lista **Retornar Colunas** e clique em **OK**:  
  
    -   Data do Pedido  
  
    -   Due Date  
  
    -   Ship Date  
  
    A imagem a seguir mostra essas colunas selecionadas.  
  
    ![Caixa colunas de detalhamento](../analysis-services/media/l8-action7.gif "caixa colunas de detalhamento")  
  
## <a name="reviewing-the-modified-drillthrough-action"></a>Revisando a ação de detalhamento modificada  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação for concluída com êxito, mude para a guia **Navegador** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique no botão **Reconectar** .  
  
3.  Inicie o Excel.  
  
4.  Recrie a Tabela Dinâmica usando **Vendas pela Internet/Valor das Vendas** na área Valores e **Geografia do Cliente** no Filtro de Relatório.  
  
    Adicione um filtro que seleciona de **Todos os Clientes**, **Austrália**, **Queensland**, **Brisbane**, **4000**e **Adam Powell**.  
  
5.  Clique na célula de dados **Vendas pela Internet/Valor das Vendas** , aponte para **Ações Adicionais**e clique em **Detalhamento até Detalhes do Pedido**.  
  
    Os detalhes dos pedidos enviados a Adam Powell serão exibidos em uma planilha temporária. Isso inclui descrição do item, número do pedido, data do pedido, data de vencimento e data de envio, como mostra a imagem a seguir.  
  
    ![Pedidos enviados a Adam Powell](../analysis-services/media/l8-action8.gif "pedidos enviados a Adam Powell")  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 9: Definindo perspectivas e traduções](../analysis-services/lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>Consulte também  
[Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)  
[Ações em modelos multidimensionais](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
[Relações de dimensão](../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
[Definindo uma relação de fatos](../analysis-services/lesson-5-2-defining-a-fact-relationship.md)  
[Definir uma relação de fato e propriedades de relação de fato](../analysis-services/multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
  
