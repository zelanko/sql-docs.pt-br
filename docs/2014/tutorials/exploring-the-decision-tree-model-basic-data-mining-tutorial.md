---
title: Explorando o modelo de árvore de decisão (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 2e1472c2-3f3e-4dae-acb3-62fca374d397
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 45acf7bef608bb23d697fc18381872f741cc2e21
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401361"
---
# <a name="exploring-the-decision-tree-model-basic-data-mining-tutorial"></a>Explorando o modelo de árvore de decisão (Tutorial de mineração de dados básico)
  O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)] prevê que colunas influenciam a decisão de compra de uma bicicleta com base nas colunas restantes do conjunto de treinamento.  
  

  
##  <a name="Decision_Tree_Tab"></a> Guia árvore de decisão  
 Sobre o **árvore de decisão** guia, você pode exibir árvores de decisão para cada atributo previsível no conjunto de dados.  
  
 Nesse caso, o modelo prevê somente uma coluna, comprador de bicicleta, portanto, há apenas uma única árvore para exibir. Se houver mais árvores, você pode usar o **árvore** caixa para escolher outra árvore.  
  
 Quando você exibir o `TM_Decision_Tree` modelo no Visualizador de árvore de decisão, você pode ver os atributos mais importantes no lado esquerdo do gráfico. "Mais importantes" significa que esses atributos têm a maior influência no resultado. Os atributos mais abaixo na árvore (à direita do gráfico) têm menos influência.  
  
 Neste exemplo, a idade é o fator mais importante na previsão da compra de bicicletas. O modelo agrupa os clientes por idade e depois mostra o próximo atributo mais importante de cada faixa etária. Por exemplo, no grupo de clientes com idades entre 34 e 40 anos, o número de carros é o fator de previsão mais importante depois da idade.  
  
#### <a name="to-explore-the-model-in-the-decision-tree-tab"></a>Para explorar o modelo na guia Árvore de Decisão  
  
1.  Selecione o **Visualizador do modelo de mineração** guia **Designer de mineração de dados**.  
  
     Por padrão, o designer é aberto para o primeiro modelo que foi adicionado à estrutura-- nesse caso, `TM_Decision_Tree`.  
  
2.  Use os botões de lente de aumento para ajustar o tamanho da exibição da árvore.  
  
     Por padrão, o Visualizador de Árvore da [!INCLUDE[msCoName](../includes/msconame-md.md)] mostra somente os três primeiros níveis da árvore. Se a árvore tiver menos de três níveis, o visualizador mostrará só os níveis existentes. Você pode exibir mais níveis usando o **Mostrar nível** controle deslizante ou a **expansão padrão** lista.  
  
3.  Deslize **Mostrar nível** até a quarta barra.  
  
4.  Alterar o **plano de fundo** valor `1`.  
  
     Alterando a **plano de fundo** definir, você pode ver rapidamente o número de casos em cada nó que têm o valor de destino `1` para [comprador de bicicleta]. Lembre-se de que neste cenário específico, cada caso representa um cliente. O valor `1` indica que o cliente anteriormente comprou uma bicicleta; o valor **0** indica que o cliente não comprou uma bicicleta. Quanto mais escuro for o sombreamento do nó, maior será a porcentagem de casos desse nó com o valor de destino.  
  
5.  Coloque o cursor sobre o nó rotulado **todos os**. Uma dica de ferramenta será exibida com as seguintes informações:  
  
    -   Número total de casos  
  
    -   Número de casos de pessoas que não compram bicicleta  
  
    -   Número de casos de compradores de bicicleta  
  
    -   Número de casos com valores ausentes para [Comprador de Bicicleta]  
  
     Como alternativa, coloque o seu cursor sobre qualquer nó da árvore para ver a condição exigida para alcançar aquele nó a partir do nó anterior. Você também pode exibir essas informações na **legenda de mineração**.  
  
6.  Clique no nó para **idade > = 34 e < 41**. O histograma é exibido como uma barra horizontal final no nó e representa a distribuição de clientes nesse intervalo de idade que compraram (rosa) e que não compraram (azul) uma bicicleta anteriormente. O Visualizador nos mostra que os clientes entre os 34 e os 40 anos com um ou nenhum carro têm probabilidade de comprar uma bicicleta. Levando isso um pouco mais adiante, descobrimos que a probabilidade de compra de uma bicicleta aumenta caso o cliente tenha realmente entre 38 e 40 anos.  
  
 Como você habilitou o detalhamento quando criou a estrutura e o modelo, poderá recuperar informações detalhadas dos casos de modelo e da estrutura de mineração, incluindo as colunas não incluídas no modelo de mineração (por exemplo, emailAddress, FirstName).  
  
 Para obter mais informações, consulte [Consultas de detalhamento &#40;Mineração de dados&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-drill-through-to-case-data"></a>Para detalhar os dados de caso  
  
1.  Um nó com o botão direito e selecione **Detalhar** , em seguida, **colunas do modelo somente**.  
  
     Os detalhes para cada caso de treinamento são exibidos em formato de planilha. Esses detalhes vêm da exibição vTargetMail, selecionada como a tabela de caso durante a criação da estrutura de mineração.  
  
2.  Um nó com o botão direito e selecione **Detalhar** , em seguida, **colunas do modelo e estrutura**.  
  
     A mesma planilha será exibida com as colunas da estrutura anexadas no final.  
  
  
###  <a name="Dependency_Network_Tab"></a> Guia rede de dependências  
 O **rede de dependências** guia exibe as relações entre os atributos que contribuem para a capacidade de previsão do modelo de mineração. O visualizador Rede de Dependências reforça as nossas descobertas de que Idade e Região são fatores importantes na previsão de compra de bicicletas.  
  
##### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Para explorar o modelo na guia Rede de Dependências  
  
1.  Clique o `Bike Buyer` nó para identificar suas dependências.  
  
     O nó central para a rede de dependências, `Bike Buyer`, representa o atributo previsível no modelo de mineração. O gráfico destaca todos os nós conectados que têm um efeito sobre o atributo previsível.  
  
2.  Ajustar a **todos os Links** controle deslizante para identificar o atributo mais influente.  
  
     Quando você arrasta para baixo o controle deslizante, atributos que têm apenas um efeito menor na coluna [Bike Buyer] são removidos do gráfico. Ao ajustar o controle deslizante, você poderá descobrir que Idade e Região são os principais fatores para prever se alguém é um comprador de bicicletas.  
  
## <a name="related-tasks"></a>Related Tasks  
 Consulte estes tópicos para explorar os dados usando outros tipos de modelos.  
  
-   [Explorando o modelo de Clustering &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Explorando o modelo Naive Bayes &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Explorando o modelo de Clustering &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do visualizador do modelo de mineração](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Guia árvore de decisão &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/decision-tree-tab-mining-model-viewer.md)   
 [Guia rede de dependências &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)   
 [Procurar um modelo usando a Exibição de Árvore da Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
  
