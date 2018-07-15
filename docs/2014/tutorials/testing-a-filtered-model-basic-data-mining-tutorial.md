---
title: Testando um modelo filtrado (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87af6785855f81abcffe57e3672e59fcf00b5e2b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319726"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>Testando um modelo filtrado (Tutorial de mineração de dados básico)
  Agora que você determinou que o `TM_Decision_Tree` modelo é o mais preciso, você personalizará o modelo para atender melhor às necessidades do [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] campanha de mala. Especificamente, o departamento de marketing gostaria de saber se existe alguma diferença entre os clientes masculino e feminino. As informações podem ajudá-los a decidir que revistas a ser usado para propaganda e que produtos em suas malas diretas.  
  
## <a name="using-filters"></a>Usando filtros  
 A filtragem permite que você crie com facilidade modelos criados com base em subconjuntos de seus dados. O filtro só é aplicado ao modelo e não altera a fonte de dados subjacente.  
  
 Nesta lição, você criará um modelo filtrado por gênero, para prever as características que mais influenciam no comportamento de compra em homens e mulheres.  
  
 Primeiro, você fará uma cópia do `TM_Decision_Tree` modelo.  
  
#### <a name="to-copy-the-decision-tree-model"></a>Para copiar o modelo de árvore de decisão  
  
1.  Na [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no Gerenciador de soluções, selecione **BasicDataMining**.  
  
2.  Clique na guia **Modelos de Mineração** .  
  
3.  Clique com botão direito do `TM_Decision_Tree` de modelo e, em seguida, selecione **novo modelo de mineração.**  
  
4.  No **nome do modelo** , digite `TM_Decision_Tree_Male`.  
  
5.  Clique em **OK**.  
  
 Em seguida, crie um filtro para selecionar clientes para o modelo baseado em gênero.  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>Para criar um filtro de caso em um modelo de mineração  
  
1.  Clique com botão direito do `TM_Decision_Tree_Male` modelo de mineração para abrir o menu de atalho.  
  
     – ou –  
  
     Selecione o modelo. No menu **Modelo de Mineração** , selecione **Definir Filtro de Modelos**.  
  
2.  Na caixa de diálogo **Filtro de Modelos** , clique na linha superior da grade, na caixa de texto **Coluna da Estrutura de Mineração** .  
  
     A lista suspensa só exibe os nomes das colunas dessa tabela.  
  
3.  Na caixa de texto coluna da estrutura de mineração, selecione **gênero**.  
  
     O ícone no lado esquerdo da caixa de texto muda para indicar que o item selecionado é uma tabela ou uma coluna.  
  
4.  Clique o **operador** caixa de texto e selecione o operador de igual (=) na lista.  
  
5.  Clique o **valor** caixa de texto e digite **M**.  
  
6.  Na grade, clique na linha seguinte.  
  
7.  Clique em **Okey** para fechar o **filtro de modelos** caixa de diálogo.  
  
     O filtro exibe a **propriedades** janela. Como alternativa, você pode iniciar o **filtro de modelos** caixa de diálogo da **propriedades** janela.  
  
8.  Repita as etapas acima, mas desta vez chame o modelo `TM_Decision_Tree_Female` e digite **F** no **valor** caixa de texto.  
  
## <a name="process-the-filtered-models"></a>Processar os modelos filtrados  
 Os modelos só poderão ser usados depois de serem implantados e processados. Para obter mais informações sobre o processamento de modelos, consulte [processando modelos na estrutura de mala direta direcionada &#40;Tutorial básico de mineração de dados&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md).  
  
#### <a name="to-process-the-filtered-model"></a>Para processar o modelo filtrado  
  
1.  Clique com botão direito do `TM_Decision_Tree_Male` de modelo e selecione **processar estrutura de mineração e todos os modelos**s  
  
2.  Clique em **executar** para processar os novos modelos.  
  
3.  Depois que o processamento for concluído, clique em **fechar** nas duas janelas de processamento.  
  
     Agora você tem dois novos modelos exibidos na **modelos de mineração** guia.  
  
## <a name="evaluate-the-results"></a>Avaliar os resultados.  
 Examine os resultados e avalie a precisão dos modelos filtrados da mesma forma como foi feito nos três modelos anteriores. Para obter mais informações, consulte:  
  
 [Explorando o modelo de árvore de decisão &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [Testando a precisão com gráficos de comparação &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>Para explorar os modelos filtrados  
  
1.  Selecione o **Visualizador do modelo de mineração** guia **Designer de mineração de dados**.  
  
2.  Na caixa de modelo de mineração, selecione `TM_Decision_Tree_Male`.  
  
3.  Deslize **Mostrar nível** para `3`.  
  
4.  Alterar o **plano de fundo** valor `1`.  
  
5.  Coloque o cursor sobre o nó rotulado **todos os** para ver o número de compradores de bicicleta versus não compradores de bicicleta.  
  
6.  Repita as etapas 1 a 5 para `TM_Decision_Tree_Female`.  
  
7.  Explorar os resultados para o `TM_Decision_Tree` e dos modelos filtrados por gênero. Em comparação a todos os compradores de bicicleta, os compradores de bicicleta homens e mulheres compartilham as mesmas características dos compradores de bicicleta não filtrados, mas todos os três também possuem diferenças interessantes. Essas informações são úteis que [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] pode usar para desenvolver sua campanha de marketing.  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>Para testar a comparação de precisão dos modelos filtrados  
  
1.  Alterne para o **gráfico de precisão de mineração** guia no Designer de mineração de dados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e selecione o **seleção de entrada** guia.  
  
2.  No **Selecionar conjunto de dados a ser usado para gráfico de precisão** caixa de grupo, selecione **usar casos de teste da estrutura de mineração**.  
  
3.  Sobre o **seleção de entrada** guia do Designer de mineração de dados, em **selecionar colunas do modelo de mineração previsíveis para mostrar no gráfico de comparação**, marque a caixa de seleção **sincronizar colunas de previsão e Valores**.  
  
4.  No **nome da coluna previsível** coluna, verifique **comprador de bicicleta** está selecionada para cada modelo.  
  
5.  No **Mostrar** coluna, selecione cada um dos modelos.  
  
6.  No **valor de previsão** coluna, selecione `1`.  
  
7.  Selecione o **gráfico de comparação de precisão** guia para exibir o gráfico de comparação de precisão.  
  
     Você observará que todos os três modelos de Árvore de Decisão oferecem uma precisão significativa comparado com o modelo de previsão aleatório, além de superarem os modelos Clustering e Naive Bayes.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre filtros, consulte [filtros para modelos de mineração &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Para obter um exemplo de como aplicar filtros a tabelas aninhadas, consulte [Tutorial intermediário de mineração de dados &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md).  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Testando a precisão com gráficos de comparação &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 6: Criando e trabalhando com previsões &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tutorial de mineração de dados intermediário &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Tarefas e tarefas do modelo de mineração](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Excluir um filtro de um modelo de mineração](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [Filtros para modelos de mineração &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
