---
title: Guia discriminação do cluster de clustering de sequências (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.discrimination.f1
ms.assetid: 7dd16479-2633-4f4b-83bf-cf55972a2241
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 914629fca09d4bcffb5ac931316331bbb7e7eebe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069142"
---
# <a name="sequence-clustering-cluster-discrimination-tab-mining-model-viewer"></a>Guia Discriminação de Cluster do clustering de sequências (Visualizador do Modelo de Mineração)
  A guia  **Discriminação do Cluster** no **Visualizador de Cluster de Sequência da Microsoft** compara clusters selecionados de um modelo de clustering de sequências.  
  
 Use esta exibição de um modelo de clustering de sequência para comparar dois clusters e ver quais estados e transições são diferentes.  
  
 **Para obter mais informações:** [algoritmo de clustering de sequência da Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md), [procurar um modelo usando o Visualizador de cluster de sequência da Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibir o que está presente na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador que será usado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado, ou o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Você também pode usar visualizadores de plug-in se houver.  
  
 **Cluster 1**  
 Selecione um cluster desses no modelo.  
  
 **Cluster 2**  
 Selecione um segundo cluster no modelo de mineração para comparar com o **Cluster 1**.  
  
 Se você não selecionar outro cluster, por padrão o cluster selecionado será comparado com seu complemento, ou seja, todos os casos no modelo que não estão no Cluster 1.  
  
 **Pontuações de \<discriminação para cluster 1 \<> e cluster 2>**  
 Este gráfico fornece a comparação detalhada dos clusters que você selecionou. Em geral, um modelo de clustering raramente atribui estados ou valores exclusivamente a um único cluster. Portanto, o visualizador apenas indica que um atributo específico ou estado *favorece* um cluster específico.  
  
 Em geral, um determinado cluster pode conter mais de um estado: por exemplo, um estado comum pode ser a compra de uma Garrafa de Água e Suporte de Garrafa de Água na sequência. Porém, a sequência pode estar presente em outros clusters que têm características de definição mais importantes. Por exemplo, outro cluster pode ser caracterizado mais fortemente por tempos de transação muito curtos, e uma análise revelaria que os itens Garrafa de Água e Suporte de Garrafa de Água estão posicionados para geralmente poderem ser agrupados neste cluster, mas não sempre.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Variáveis**|Um atributo no modelo de mineração.|  
|**Valores**|Um estado do atributo listado em **Variáveis**.|  
|**Favorece \<o cluster 1>**|Contém uma barra sombreada que indica a força de o atributo e o estado listados em **Variáveis** e **Valor** favorecerem o cluster selecionado em **Cluster 1.**|  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining/data-mining-model-viewers.md)  
  
  
