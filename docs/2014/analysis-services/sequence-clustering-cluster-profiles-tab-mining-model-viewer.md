---
title: Guia Perfis de Cluster de Clustering de sequências (Visualizador do modelo de mineração | Microsoft Docs
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
- sql12.dm.miningmodeleditor.sequenceclustering.profiles.f1
ms.assetid: 44230895-0a42-4032-8d6c-0cdb8a2dbb8c
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b69066bd09f74fddd0fc7151eae216b74444e8f0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323126"
---
# <a name="sequence-clustering-cluster-profiles-tab-mining-model-viewer"></a>Guia Perfis de Cluster do clustering de sequências (Visualizador do Modelo de Mineração)
  A guia **Perfis de Cluster** no **Visualizador MSC** fornece uma exibição codificada por cores das sequências que são incluídas em cada cluster.  
  
 Use esta exibição de um modelo de clustering de sequência para obter uma exibição rápida de como são agrupadas as sequências localizadas pelo modelo. Você pode ver à primeira vista quantas sequências são longas e quantas são curtas. Você pode também clicar em um cluster e exibir a **Legenda de mineração** para ver exatamente quais estados as cores em cada sequência representam.  
  
 **Para obter mais informações:**[algoritmo msc](data-mining/microsoft-sequence-clustering-algorithm.md), [procurar um modelo usando o Visualizador de Cluster de sequência da Microsoft  ](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibir o que está presente na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador que será usado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado, ou o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Você também pode usar visualizadores de plug-in se houver.  
  
 **Mostrar legenda**  
 Selecione esta opção para exibir uma legenda que mostra a correlação entre as cores exibidas nos perfis de cluster e os valores de texto dos estados.  
  
 **Barras de histograma**  
 Use esta opção para alterar o número de barras coloridas que estão incluídas no histograma. Caso haja mais barras do que você optou por exibir, as barras mais importantes serão retidas e as restantes serão agrupadas em **Outro**.  
  
 **Atributos** e **Perfis de Cluster**  
 Esta seção do gráfico lista os clusters de sequências que foram localizados no modelo.  
  
 Cada cluster de sequência é exibido usando o número de estados selecionado na opção **Barras de histograma**.  
  
 Dois conjuntos de histogramas são exibidos para cada cluster no modelo, cada em uma linha diferente no gráfico:  
  
-   **\<nome do atributo > Attribute**: os histogramas nesta linha mostram as sequências de itens que são representativas de cada cluster. Nos termos do DMX, estes são os casos de exemplo para cada cluster.  
  
-   **\<nome do atributo >**: os histogramas nesta linha descrevem todos os itens contidos no cluster e sua distribuição geral. Clique em um histograma quando **Legenda de Mineração** estiver visível e você puder ver os valores numéricos para cada  
  
 **Estados**  
 Esta coluna no gráfico é opcional e pode ser exibida ou removida selecionando a opção **Mostrar Legenda** . A coluna **Estados** fornece um guia sobre qual estado é representado por qual cor no histograma de clusters correspondente.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Algoritmo msc](data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de mineração de dados](data-mining/data-mining-model-viewers.md)   
 [Procurar um modelo usando o Visualizador de Cluster de Sequência da Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
