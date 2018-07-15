---
title: Guia árvore (Visualizador do modelo de mineração) de decisão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.decisiontree.f1
ms.assetid: dc88606f-ba7c-4f8d-af65-bfa17ec16e2b
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 86c229c4adc57200a2d1867c167aa3d998498765
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37276332"
---
# <a name="decision-tree-tab-mining-model-viewer"></a>Guia Árvore de Decisão (Visualizador do Modelo de Mineração)
  O painel **DecisionTree** exibe uma representação visual das regras de decisão criadas em um modelo de árvore de decisão. As regras de decisão descrevem caminhos para um determinado resultado.  
  
 **Para obter mais informações:** [Algoritmo Árvores de Decisão da Microsoft](data-mining/microsoft-decision-trees-algorithm.md), [Procurar um modelo usando o Visualizador de Árvore da Microsoft](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração dentre eles na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado, ou Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar visualizadores de plug-in se houver.  
  
 **Ampliar**  
 Aproxime para obter uma exibição mais detalhada dos nós e das ramificações na árvore de decisão. Em um modelo complexo, as árvores de decisão podem ter muitos níveis de ramificação.  
  
 **Reduza a imagem**  
 Reduza para obter uma exibição geral da estrutura da árvore.  
  
 **Copiar exibição de gráfico**  
 Copie a seção visível do diagrama para a área de transferência.  
  
 **Copiar gráfico inteiro**  
 Copie todo o diagrama na área de transferência.  
  
 **Dimensionar diagrama para ajustar à janela**  
 Reduza o diagrama até que a estrutura de árvore inteira se ajuste na tela.  
  
 **Histogramas**  
 Selecione, para cada nó, o número de estados que podem ser exibidos no histograma. Se o número de estados no modelo for menor que o valor que você selecionar, nenhuma barra adicional será exibida.  
  
 **Árvore**  
 Escolha uma árvore para ser exibida no visualizador. Se você criar um modelo que tem vários atributos previsíveis, o algoritmo criará uma árvore separada para cada atributo previsível.  
  
 **Plano de fundo**  
 Escolha um valor do atributo previsível para ser usado na representação da cor de fundo de cada nó. Por exemplo, nos modelos de exemplo da AdventureWorks, se você definir **Segundo plano** como 1 ([Comprador de Bicicleta] = Sim), os nós serão escurecidos se tiverem uma proporção maior proporção de compradores de bicicleta. Esta opção fornece uma sugestão visual adicional sobre o significado das ramificações e nós na árvore.  
  
 **Expansão padrão**  
 Escolha um valor da lista para definir o padrão para o número de níveis exibidos no gráfico de árvore.  
  
 **Mostrar nível**  
 Mova a barra do controle deslizante para a direita ou esquerda para ajustar o número de níveis exibidos no gráfico de árvore. Para ver todos os nós no modelo, deslize a barra completamente para a direita.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  
