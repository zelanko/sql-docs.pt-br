---
title: Guia perfis de cluster (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.profiles.f1
ms.assetid: 1ebafa1f-74e9-4c05-b278-a690fa8543bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ebed4b2b7cc5c6496ab0c681450897a477e4707a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087867"
---
# <a name="cluster-profiles-tab-mining-model-viewer"></a>Guia Perfis de Cluster (Visualizador do Modelo de Mineração)
  Use a guia **Perfis de Cluster** para obter uma exibição global dos clusters que o algoritmo descobriu dentro de um modelo de clustering. A guia exibe cada atributo, junto com a distribuição do atributo em cada cluster.  
  
 **Para obter mais informações:** [Algoritmo MSC](data-mining/microsoft-clustering-algorithm.md), [Procurar um modelo usando o Visualizador de Cluster da Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração dentre eles na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador para exibir o modelo de mineração selecionado. Você pode usar o visualizador personalizado para o modelo de mineração, ou Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar visualizadores de plug-in se houver.  
  
 **Mostrar Legenda**  
 Escolha esta opção para exibir uma chave que mostra o mapeamento de cores no visualizador para valores na coluna **Estados** .  
  
 **Barras de histograma**  
 Altere este valor para controlar quantos estados estão incluídos em cada histograma. Se houver mais estados do que você opte por exibir, os estados de maior importância serão mostrados no histograma e os restantes serão agrupados em **Outras**.  
  
 **Atributos**  
 Lista as colunas que estão no modelo de clustering. Os histogramas para cada atributo mostram como ele é distribuído entre os clusters identificados pelo algoritmo.  
  
 **Estados**  
 Fornece uma chave que denota que cor representa cada estado na linha de clusters correspondente, ou um controle deslizante com losango que indica a distribuição de valores numéricos contínuos. Você pode mostrar ou ocultar esta coluna usando a caixa de seleção **Mostrar Legenda** .  
  
 **Perfis de cluster**  
 Esta seção contém uma coluna para cada cluster no modelo. Para cada atributo, o histograma mostra a distribuição dos valores no atributo somente para esse cluster. O gráfico também tem uma coluna para **População**, que também usa histogramas para exibir a distribuição de valores para cada atributo, mas para todos os casos no modelo.  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining/data-mining-model-viewers.md)  
  
  
