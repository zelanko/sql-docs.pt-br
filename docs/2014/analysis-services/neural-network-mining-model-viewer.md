---
title: Rede neural (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.neuralnet.f1
ms.assetid: 18d87e7b-a821-40ea-9bd8-c6fecf189a1c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05654d9206f09d151abd5557d0aa6aae90b1b9ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072315"
---
# <a name="neural-network-mining-model-viewer"></a>Rede Neural (Visualizador do Modelo de Mineração)
  Use o visualizador da **Rede Neural** para explorar modelos de mineração que sejam baseados no algoritmo Rede Neural da [!INCLUDE[msCoName](../includes/msconame-md.md)] ou no algoritmo Regressão Logística da [!INCLUDE[msCoName](../includes/msconame-md.md)] .  
  
 **Para obter mais informações:** [algoritmo de rede neural](data-mining/microsoft-neural-network-algorithm.md)da Microsoft, [algoritmo de regressão logística da Microsoft](data-mining/microsoft-logistic-regression-algorithm.md),[procurar um modelo usando o Visualizador de rede neural da Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração a ser exibido, dentre eles na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado, ou o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Você também pode usar visualizadores de plug-in se houver.  
  
 **Entrada**  
 Use esta área para escolher atributos de entrada e valores, para que você possa explorar posteriormente como eles afetam o resultado.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Attribute**|Escolha um atributo de entrada na lista. Se você deixar a seleção como padrão, ** \<todos os>**, o gráfico mostrará uma lista de todos os atributos de entrada, classificados por seu impacto sobre o atributo previsível.|  
|**Valor**|Escolha um valor para o atributo de entrada.|  
  
 **Saída**  
 Use estes controles para escolher um atributo previsível e um valor para analisar e comparar no gráfico de barras. Se você não alterar as seleções, o gráfico de barras comparará os dois principais estados de resultado.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Atributo de Saída**|Escolha um atributo previsível. Se você não definiu a coluna como previsível ao criar o modelo, não poderá adicioná-la aqui.|  
|**Valor 1**|Escolha um estado do atributo previsível a ser comparado com a condição que está contida em **Valor 2**.<br /><br /> Você pode comparar dois valores discretos ou diferenciados; porém, não pode comparar um valor com seu complemento, como pode em outros visualizadores.|  
|**Valor 2**|Selecione o estado do atributo previsível a ser comparado com o estado que está contido em **Valor 1**.|  
  
 **Variáveis**  
 Esta parte da guia **Rede Neural** contém um gráfico de barras interativo que responde às seleções que você fez para atributos de entrada e de resultado. Como uma rede neural calcula a probabilidade de um valor específico influenciar um resultado específico, você pode escolher qualquer combinação de entradas e o gráfico de barras exibirá como essa combinação afetará o par de resultados que você está comparando.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Attribute**|Mostra o nome do atributo de entrada selecionado em **Atributo**.|  
|**Valor**|Mostra o valor para o atributo de entrada selecionado.|  
|**Favorece \<o valor 1>**|Exibe uma barra que indica quanto esta combinação específica de atributo e valor afeta o resultado de destino escolhido em **Valor 1**.|  
|**Favorece \<o valor 2>**|Exibe uma barra que indica quanto esta combinação específica de atributo e valor afeta o resultado de destino escolhido em **Valor 2**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining/data-mining-model-viewers.md)  
  
  
