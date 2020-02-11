---
title: Filtrando uma tabela aninhada em um modelo de mineração (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0a3ae0e5-897b-4898-a60d-5455eec3d305
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f57d691587d658e968cd79cf4f4ab4731db29915
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63267474"
---
# <a name="filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial"></a>Filtrando uma tabela aninhada em um modelo de mineração (tutorial de mineração de dados intermediário)
  Após criar e explorar o modelo, você decide que deseja enfatizar um subconjunto dos dados do cliente. Por exemplo, talvez você queira analisar apenas as cestas que contêm um determinado item ou os dados demográficos de clientes que não compraram nada em um certo período.  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece a capacidade para filtrar os dados que são usados em um modelo de mineração. Esse recurso é útil porque você não precisa configurar uma nova exibição da fonte de dados para usar dados diferentes. No Tutorial de mineração de dados básico, você aprendeu a filtrar dados de uma tabela simples aplicando condições à tabela de casos. Nesta tarefa, você criará um filtro que se aplica a uma tabela aninhada.  
  
## <a name="filters-on-nested-vs-case-tables"></a>Filtros em tabelas aninhadas vs. tabelas de casos  
 Se a sua exibição de fonte de dados contiver uma tabela de casos e uma tabela aninhada, como a exibição da fonte de dados usada no modelo de Associação, você poderá filtrar os valores da tabela de casos, a presença ou a ausência de um valor na tabela aninhada ou uma combinação de ambos.  
  
 Nesta tarefa, primeiro você fará uma cópia do modelo de Associação e depois adicionará os atributos IncomeGroup e Region ao novo modelo relacionado, para que possa filtrar os atributos na tabela de casos.  
  
#### <a name="to-create-and-modify-a-copy-of-the-association-model"></a>Para criar e modificar uma cópia do modelo de Associação  
  
1.  Na guia **modelos de mineração** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com o botão `Association` direito do mouse no modelo e selecione **novo modelo de mineração**.  
  
2.  Para **nome do modelo**, `Association Filtered`digite. Para **nome do algoritmo**, selecione **regras de associação da Microsoft**. Clique em **OK**.  
  
3.  Na coluna para o modelo filtrado de associação, clique na linha do Associationgroup e altere o valor de **ignorar** para **entrada**.  
  
 Em seguida, você criará um filtro na tabela de casos no novo modelo de associação. O filtro passará ao modelo apenas os clientes na região de destino ou com o nível de renda de destino. Depois, você adicionará um segundo conjunto de condições de filtro para especificar se o modelo usa apenas clientes cujas cestas de compras continham pelo menos um item.  
  
#### <a name="to-add-a-filter-to-a-mining-model"></a>Para adicionar um filtro a um modelo de mineração  
  
1.  Na guia **modelos de mineração** , clique com o botão direito do mouse na associação de modelo filtrada e selecione **definir filtro de modelo**.  
  
2.  Na caixa de diálogo **Filtro de Modelos** , clique na linha superior da grade, na caixa de texto **Coluna da Estrutura de Mineração** .  
  
3.  Na caixa de texto **coluna da estrutura de mineração** , selecione invir.  
  
     O ícone no lado esquerdo da caixa de texto é alterado para indicar que o item selecionado é uma coluna.  
  
4.  Clique na caixa de texto **operador** e selecione **=** o operador na lista.  
  
5.  Clique na caixa de texto **valor** e digite `High` na caixa.  
  
6.  Na grade, clique na linha seguinte.  
  
7.  Clique na caixa de texto **e/ou** na próxima linha da grade e selecione **ou**.  
  
8.  Na caixa de texto **coluna da estrutura de mineração** , selecione invir. Na caixa de texto **valor** , digite `Moderate`.  
  
     A condição de filtro que você criou é automaticamente adicionada à caixa de texto **expressão** e deve aparecer da seguinte maneira:  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate'`  
  
9. Clique na próxima linha da grade, deixando o operador como o padrão **e**.  
  
10. Para **operador**, deixe o valor padrão, **contém**. Clique na caixa de texto **valor** .  
  
11. Na caixa de diálogo **filtro** , na primeira linha na **coluna estrutura de mineração**, selecione `Model`.  
  
12. Para **operador**, Select **não é nulo**. Deixe a caixa de texto **valor** em branco. Clique em **OK**.  
  
     A condição de filtro na caixa de texto **expressão** da caixa de diálogo **filtro de modelo** é atualizada automaticamente para incluir a nova condição na tabela aninhada. A expressão completa é a seguinte:  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate' AND EXISTS SELECT * FROM [vAssocSeqLineItems] WHERE [Model] <> NULL).`  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)] ``  
  
#### <a name="to-enable-drillthrough-and-to-process-the-filtered-model"></a>Para habilitar a busca detalhada e processar o modelo filtrado  
  
1.  Na guia **modelos de mineração** , clique com o botão `Association Filtered` direito do mouse no modelo e selecione **Propriedades**.  
  
2.  Altere a propriedade **AllowDrillThrough** para **true**.  
  
3.  Clique com o botão `Association Filtered` direito do mouse no modelo de mineração e selecione **modelo de processo**.  
  
4.  Clique em **Sim** na mensagem de erro para implantar o novo modelo no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados.  
  
5.  Na caixa de diálogo **processar estrutura de mineração** , clique em **executar**.  
  
6.  Quando o processamento estiver concluído, clique em **fechar** para sair da caixa de diálogo **progresso do processo** e clique em **Fechar** novamente para sair da caixa de diálogo **processar estrutura de mineração** .  
  
 Para verificar, use o visualizador da Árvore de Conteúdo Genérico da Microsoft e examine o valor de NODE_SUPPORT em que o modelo filtrado contém menos casos do que o original.  
  
## <a name="remarks"></a>Comentários  
 O filtro de tabela aninhada que você acabou de criar verifica apenas a presença de pelo menos uma linha na tabela aninhada; no entanto, também é possível criar condições de filtro que verificam a presença de produtos específicos.  Por exemplo, você pode criar o seguinte filtro:  
  
```  
[IncomeGroup] = 'High' AND  
 EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] = 'Water Bottle' )   
```  
  
 Esta instrução significa que você está restringindo os clientes da tabela de casos a apenas aqueles que compraram uma garrafa de água. No entanto, como o número de atributos da tabela aninhada é potencialmente ilimitado, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não fornece a lista dos possíveis valores a serem selecionados. Em vez disso, você deve digitar o valor exato.  
  
 Você pode clicar em **Editar consulta** para alterar manualmente a expressão de filtro. No entanto, se você alterar manualmente qualquer parte da expressão de filtro, a grade será desabilitada e, assim sendo, você deverá trabalhar com a expressão de filtro apenas no modo de edição de texto. Para restaurar o modo de edição da grade, você deve apagar a expressão de filtro e iniciar novamente.  
  
> [!WARNING]  
>  Você não pode usar o operador LIKE em um filtro de tabela aninhada.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Prevendo associações &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Sintaxe de filtro de modelo e exemplos &#40;mineração de dados Analysis Services&#41;](../../2014/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [Filtros para modelos de mineração &#40;mineração de dados Analysis Services&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
