---
title: Testando um modelo filtrado (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa4910b2849c4eb2dd04c6d0115c83683ee8bea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044061"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>Testando um modelo filtrado (Tutorial de mineração de dados básico)
  Agora que você determinou que o `TM_Decision_Tree` modelo é o mais preciso, você personalizará o modelo para se adequar melhor às necessidades [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] da campanha de mala direta. Especificamente, o departamento de marketing gostaria de saber se existe alguma diferença entre os clientes masculino e feminino. As informações podem ajudá-los a decidir que revistas serão usadas para a propaganda e que produtos deverão ser incluídos em suas malas diretas.  
  
## <a name="using-filters"></a>Usando filtros  
 A filtragem permite que você crie com facilidade modelos criados com base em subconjuntos de seus dados. O filtro só é aplicado ao modelo e não altera a fonte de dados subjacente.  
  
 Nesta lição, você criará um modelo filtrado por gênero, para prever as características que mais influenciam no comportamento de compra em homens e mulheres.  
  
 Primeiro, você fará uma cópia do `TM_Decision_Tree` modelo.  
  
#### <a name="to-copy-the-decision-tree-model"></a>Para copiar o modelo de árvore de decisão  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], em Gerenciador de soluções, selecione **BasicDataMining**.  
  
2.  Clique na guia **Modelos de Mineração** .  
  
3.  Clique com o `TM_Decision_Tree` botão direito do mouse no modelo e selecione **novo modelo de mineração.**  
  
4.  No campo **nome do modelo** , digite `TM_Decision_Tree_Male`.  
  
5.  Clique em **OK**.  
  
 Em seguida, crie um filtro para selecionar clientes para o modelo baseado em gênero.  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>Para criar um filtro de caso em um modelo de mineração  
  
1.  Clique com o botão `TM_Decision_Tree_Male` direito do mouse no modelo de mineração para abrir o menu de atalho.  
  
     -- ou --  
  
     Selecione o modelo. No menu **Modelo de Mineração** , selecione **Definir Filtro de Modelos**.  
  
2.  Na caixa de diálogo **Filtro de Modelos** , clique na linha superior da grade, na caixa de texto **Coluna da Estrutura de Mineração** .  
  
     A lista suspensa só exibe os nomes das colunas dessa tabela.  
  
3.  Na caixa de texto coluna da estrutura de mineração, selecione **sexo**.  
  
     O ícone no lado esquerdo da caixa de texto muda para indicar que o item selecionado é uma tabela ou uma coluna.  
  
4.  Clique na caixa de texto **operador** e selecione o operador igual (=) na lista.  
  
5.  Clique na caixa de texto **valor** e digite **M**.  
  
6.  Na grade, clique na linha seguinte.  
  
7.  Clique em **OK** para fechar a caixa de diálogo **filtro de modelo** .  
  
     O filtro é exibido na janela **Propriedades** . Como alternativa, você pode iniciar a caixa de diálogo **filtro de modelo** na janela **Propriedades** .  
  
8.  Repita as etapas acima, mas desta vez Nomeie o modelo `TM_Decision_Tree_Female` e digite **F** na caixa de texto **valor** .  
  
## <a name="process-the-filtered-models"></a>Processar os modelos filtrados  
 Os modelos só poderão ser usados depois de serem implantados e processados. Para obter mais informações sobre modelos de processamento, consulte [processando modelos na estrutura de mala direta direcionada &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md).  
  
#### <a name="to-process-the-filtered-model"></a>Para processar o modelo filtrado  
  
1.  Clique com o botão `TM_Decision_Tree_Male` direito do mouse no modelo e selecione **processar estrutura de mineração e todos os modelos**s  
  
2.  Clique em **executar** para processar os novos modelos.  
  
3.  Após a conclusão do processamento, clique em **fechar** em ambas as janelas de processamento.  
  
     Agora você tem dois novos modelos exibidos na guia **modelos de mineração** .  
  
## <a name="evaluate-the-results"></a>Avaliar os resultados.  
 Examine os resultados e avalie a precisão dos modelos filtrados da mesma forma como foi feito nos três modelos anteriores. Para obter mais informações, consulte:  
  
 [Exploração do modelo de árvore de decisão &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [Testando a exatidão com gráficos de comparação de precisão &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>Para explorar os modelos filtrados  
  
1.  Selecione a guia **Visualizador do modelo de mineração** no designer de mineração de **dados**.  
  
2.  Na caixa modelo de mineração, selecione `TM_Decision_Tree_Male`.  
  
3.  Deslizar **nível** de `3`apresentação para.  
  
4.  Altere o valor de plano `1`de **fundo** para.  
  
5.  Coloque o cursor sobre o nó rotulado **tudo** para ver o número de compradores de bicicletas versus compradores sem bicicletas.  
  
6.  Repita as etapas 1-5 `TM_Decision_Tree_Female`para.  
  
7.  Explore os resultados para o `TM_Decision_Tree` e os modelos filtrados para gênero. Em comparação a todos os compradores de bicicleta, os compradores de bicicleta homens e mulheres compartilham as mesmas características dos compradores de bicicleta não filtrados, mas todos os três também possuem diferenças interessantes. Essas são informações úteis que [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] podem ser usadas para desenvolver sua campanha de marketing.  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>Para testar a comparação de precisão dos modelos filtrados  
  
1.  Alterne para a guia **gráfico de precisão de mineração** no designer de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] mineração de dados no e selecione a guia **seleção de entrada** .  
  
2.  Na caixa de grupo **selecionar conjunto de dados a ser usado para o gráfico de precisão** , selecione **usar casos de teste da estrutura de mineração**.  
  
3.  Na guia **seleção de entrada** do designer de mineração de dados, em **selecionar colunas do modelo de mineração previsível para mostrar no gráfico**de comparação de precisão, marque a caixa de seleção para **sincronizar colunas de previsão e valores**.  
  
4.  Na coluna **nome da coluna previsível** , verifique se o **comprador de bicicleta** está selecionado para cada modelo.  
  
5.  Na coluna **Mostrar** , selecione cada um dos modelos.  
  
6.  Na coluna **valor da previsão** , selecione `1`.  
  
7.  Selecione a guia gráfico de comparação de **precisão** para exibir o gráfico de comparação de precisão.  
  
     Você observará que todos os três modelos de Árvore de Decisão oferecem uma precisão significativa comparado com o modelo de previsão aleatório, além de superarem os modelos Clustering e Naive Bayes.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre filtros, consulte [filtros para modelos de mineração &#40;&#41;de mineração de dados Analysis Services ](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Para obter um exemplo de como aplicar filtros a tabelas aninhadas, consulte [tutorial de mineração de dados intermediário &#40;Analysis Services&#41;de mineração de dados ](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md).  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Testando a exatidão com gráficos de comparação de precisão &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 6: Criando e trabalhando com previsões &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tutorial de mineração de dados intermediário &#40;Analysis Services de mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Tarefas e instruções do modelo de mineração](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Excluir um filtro de um modelo de mineração](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [Filtros para modelos de mineração &#40;mineração de dados Analysis Services&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
