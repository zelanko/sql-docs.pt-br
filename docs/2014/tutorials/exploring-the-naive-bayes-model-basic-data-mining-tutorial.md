---
title: Explorando o modelo Naive Bayes (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: eb35c829b798335a27a37629711acf299ac2c7c9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62472880"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>Explorando o modelo Naive Bayes (Tutorial de mineração de dados básico)
  O [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Naive Bayes fornece vários métodos para exibir a interação entre a compra de bicicletas e os atributos de entrada.  
  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizador do Naive Bayes fornece as seguintes guias para uso em explorando os modelos de mineração do Naive Bayes:  
  
 
  
##  <a name="dependency-network"></a><a name="DependencyNetwork"></a>Rede de dependências  
 A guia **rede de dependências** funciona da mesma maneira que a guia **rede de dependências** para o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizador de árvore. Cada nó no visualizador representa um atributo e as linhas entre os nós representam as relações. No visualizador, você pode ver todos os atributos que afetam o estado do atributo de previsão, Comprador de Bicicletas.  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Para explorar o modelo na guia Rede de Dependências  
  
1.  Use a lista **modelo de mineração** na parte superior da guia Visualizador do modelo de **mineração** para alternar `TM_NaiveBayes` para o modelo.  
  
2.  Use a lista de **visualizadores** para alternar para **o Visualizador do Microsoft Naive Bayes**.  
  
3.  Clique no `Bike Buyer` nó para identificar suas dependências.  
  
     O sombreamento rosa indica que todos os atributos influenciam a compra de bicicletas.  
  
4.  Ajuste o controle deslizante para identificar o atributo mais influente.  
  
     À medida que você abaixa o controle deslizante, somente os atributos com o efeito maior sobre a coluna [Comprador de Bicicleta] permanecem. Ao ajustar o controle deslizante, você poderá descobrir que alguns dos atributos mais influentes são: o número de carros, distância do trabalho e número total de crianças.  
 
  
##  <a name="attribute-profiles"></a><a name="AttributeProfiles"></a> Perfis de Atributo  
 A guia **perfis de atributo** descreve como Estados diferentes dos atributos de entrada afetam o resultado do atributo previsível.  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>Para explorar o modelo na guia Perfis de Atributo  
  
1.  Na caixa **previsível** , verifique se `Bike Buyer` está selecionado.  
  
2.  Se a **legenda de mineração** estiver bloqueando a exibição dos **perfis de atributo**, mova-o para fora do caminho.  
  
3.  Na caixa barras de **histograma** , selecione **5**.  
  
     Em nosso modelo, 5 é o número máximo de estados para qualquer variável.  
  
     Os atributos que afetam o estado desse atributo previsível estão listados juntos com os valores de cada estado dos atributos de entrada e suas distribuições em cada estado do atributo previsível.  
  
4.  Na coluna **atributos** , encontre **número de carros de propriedade**.  Observe as diferenças nos histogramas de compradores de bicicleta (coluna rotulada 1) e não compradores de bicicleta (coluna rotulada 0). Uma pessoa com nenhum ou com um carro tem muito mais probabilidade de comprar uma bicicleta.  
  
5.  Clique duas vezes na célula **número de carros** no comprador de bicicletas (coluna rotulada 1).  
  
     A **legenda de mineração** exibe uma exibição mais detalhada.  
  
  
##  <a name="attribute-characteristics"></a><a name="AttributeCharacteristics"></a> Características do Atributo  
 Com a guia **características do atributo** , você pode selecionar um atributo e um valor para ver com que frequência os valores de outros atributos aparecem nos casos de valores selecionados.  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>Para explorar o modelo na guia Características do Atributo  
  
1.  Na lista **atributo** , verifique se `Bike Buyer` está selecionado.  
  
2.  Defina o **valor** como **1**.  
  
     No visualizador, você verá que clientes sem filhos em casa, com pequenas distâncias até o trabalho e que moram na região da América do Norte têm mais probabilidade de comprarem uma bicicleta.  
  
  
##  <a name="attribute-discrimination"></a><a name="AttributeDiscrimination"></a> Distinção de Atributo  
 Com a guia **discriminação de atributo** , você pode investigar a relação entre dois valores discretos de compra de bicicletas e outros valores de atributo. Como o `TM_NaiveBayes` modelo tem apenas dois Estados, 1 e 0, você não precisa fazer nenhuma alteração no visualizador.  
  
 No visualizador, você pode ver que as pessoas que não têm carro tendem a comprar bicicletas, e que as pessoas que têm dois carros tendem a não comprar bicicletas.  
  
## <a name="related-tasks"></a>Related Tasks  
 Consulte os tópicos a seguir para explorar os outros modelos de mineração.  
  
-   [Exploração do modelo de árvore de decisão &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorando o modelo de clustering &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 5: testando modelos &#40;o tutorial de mineração de dados básico&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Explorando o modelo de clustering &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Procurar um modelo usando o Visualizador do Microsoft Naive Bayes](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [Guia discriminação de atributo &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [Guia perfis de atributo &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [Guia características do atributo &#40;o Visualizador do modelo de mineração&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [Guia rede de dependências &#40;Visualizador do modelo de mineração&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  
