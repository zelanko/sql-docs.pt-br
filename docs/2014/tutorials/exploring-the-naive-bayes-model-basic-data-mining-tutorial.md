---
title: Explorando o modelo Naive Bayes (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ce01a9d352513e4b69bb4a9e735f30cc657a9c97
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311854"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>Explorando o modelo Naive Bayes (Tutorial de mineração de dados básico)
  O [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Naive Bayes fornece vários métodos para exibir a interação entre a compra de bicicleta e os atributos de entrada.  
  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizador Naive Bayes fornece as seguintes guias para uso na exploração de modelos de mineração Naive Bayes:  
  
 
  
##  <a name="DependencyNetwork"></a> Rede de dependências  
 O **rede de dependências** guia funciona da mesma maneira como o **rede de dependências** guia para o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizador de árvore. Cada nó no visualizador representa um atributo e as linhas entre os nós representam as relações. No visualizador, você pode ver todos os atributos que afetam o estado do atributo de previsão, Comprador de Bicicletas.  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Para explorar o modelo na guia Rede de Dependências  
  
1.  Use o **modelo de mineração** lista na parte superior do **Visualizador do modelo de mineração** tab para alternar para o `TM_NaiveBayes` modelo.  
  
2.  Use o **visualizador** lista para alternar para **visualizador Microsoft Naive Bayes**.  
  
3.  Clique o `Bike Buyer` nó para identificar suas dependências.  
  
     O sombreamento rosa indica que todos os atributos influenciam a compra de bicicletas.  
  
4.  Ajuste o controle deslizante para identificar o atributo mais influente.  
  
     À medida que você abaixa o controle deslizante, somente os atributos com o efeito maior sobre a coluna [Comprador de Bicicleta] permanecem. Ao ajustar o controle deslizante, você poderá descobrir que alguns dos atributos mais influentes são: o número de carros, distância do trabalho e número total de crianças.  
 
  
##  <a name="AttributeProfiles"></a> Perfis de atributo  
 O **perfis de atributo** guia descreve como os diferentes estados dos atributos de entrada afetam o resultado do atributo previsível.  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>Para explorar o modelo na guia Perfis de Atributo  
  
1.  No **previsível** , verifique se que `Bike Buyer` está selecionado.  
  
2.  Se o **legenda de mineração** está bloqueando a exibição do **perfis de atributo**, movê-la do caminho.  
  
3.  No **histograma** caixa de barras, selecione **5**.  
  
     Em nosso modelo, 5 é o número máximo de estados para qualquer variável.  
  
     Os atributos que afetam o estado desse atributo previsível estão listados juntos com os valores de cada estado dos atributos de entrada e suas distribuições em cada estado do atributo previsível.  
  
4.  No **atributos** coluna, localizar **número de carros**.  Observe as diferenças nos histogramas de compradores de bicicleta (coluna rotulada 1) e não compradores de bicicleta (coluna rotulada 0). Uma pessoa com nenhum ou com um carro tem muito mais probabilidade de comprar uma bicicleta.  
  
5.  Clique duas vezes o **número de carros** célula comprador de bicicleta (coluna rotulada 1) de colunas.  
  
     O **legenda de mineração** exibe uma exibição mais detalhada.  
  
  
##  <a name="AttributeCharacteristics"></a> Características do atributo  
 Com o **características do atributo** guia, você pode selecionar um atributo e um valor para ver a frequência com valores para outros atributos aparecem nos casos de valor selecionado.  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>Para explorar o modelo na guia Características do Atributo  
  
1.  No **atributo** Verifique `Bike Buyer` está selecionado.  
  
2.  Definir o **valor** para **1**.  
  
     No visualizador, você verá que clientes sem filhos em casa, com pequenas distâncias até o trabalho e que moram na região da América do Norte têm mais probabilidade de comprarem uma bicicleta.  
  
  
##  <a name="AttributeDiscrimination"></a> Distinção de atributo  
 Com o **distinção de atributo** guia, você pode investigar a relação entre dois valores discretos de compra de bicicleta e outros valores de atributo. Porque o `TM_NaiveBayes` modelo tem apenas dois estados, 1 e 0, não é necessário fazer alterações no visualizador.  
  
 No visualizador, você pode ver que as pessoas que não têm carro tendem a comprar bicicletas, e que as pessoas que têm dois carros tendem a não comprar bicicletas.  
  
## <a name="related-tasks"></a>Related Tasks  
 Consulte os tópicos a seguir para explorar os outros modelos de mineração.  
  
-   [Explorando o modelo de árvore de decisão &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorando o modelo de Clustering &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 5: Testando modelos &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Explorando o modelo de Clustering &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Procurar um modelo usando o visualizador Microsoft Naive Bayes](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [Guia distinção de atributo &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [Guia Perfis de atributo &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [Guia características do atributo &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [Guia rede de dependências &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  