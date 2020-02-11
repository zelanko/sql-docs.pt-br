---
title: Guia perfis de cluster do clustering de sequências (Visualizador do modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.profiles.f1
ms.assetid: 44230895-0a42-4032-8d6c-0cdb8a2dbb8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f277abea585715f6a3656fffe7672f347233507
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069103"
---
# <a name="sequence-clustering-cluster-profiles-tab-mining-model-viewer"></a>Guia Perfis de Cluster do clustering de sequências (Visualizador do Modelo de Mineração)
  A guia **Perfis de Cluster** no **Visualizador MSC** fornece uma exibição codificada por cores das sequências que são incluídas em cada cluster.  
  
 Use esta exibição de um modelo de clustering de sequência para obter uma exibição rápida de como são agrupadas as sequências localizadas pelo modelo. Você pode ver à primeira vista quantas sequências são longas e quantas são curtas. Você pode também clicar em um cluster e exibir a **Legenda de mineração** para ver exatamente quais estados as cores em cada sequência representam.  
  
 **Para obter mais informações:**  [algoritmo de clustering de sequência da Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md), [procurar um modelo usando o Visualizador de cluster de sequência da Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibir o que está presente na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador que será usado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado, ou o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Você também pode usar visualizadores de plug-in se houver.  
  
 **Mostrar Legenda**  
 Selecione esta opção para exibir uma legenda que mostra a correlação entre as cores exibidas nos perfis de cluster e os valores de texto dos estados.  
  
 **Barras de histograma**  
 Use esta opção para alterar o número de barras coloridas que estão incluídas no histograma. Caso haja mais barras do que você optou por exibir, as barras mais importantes serão retidas e as restantes serão agrupadas em **Outro**.  
  
 **Atributos** e **perfis de cluster**  
 Esta seção do gráfico lista os clusters de sequências que foram localizados no modelo.  
  
 Cada cluster de sequência é exibido usando o número de estados selecionado na opção **Barras de histograma**.  
  
 Dois conjuntos de histogramas são exibidos para cada cluster no modelo, cada em uma linha diferente no gráfico:  
  
-   **nome do atributo>. Samples: os histogramas nessa linha mostram as sequências de itens que são representativos de cada cluster. \<** Nos termos do DMX, estes são os casos de exemplo para cada cluster.  
  
-   nome do atributo>: os histogramas nesta linha descrevem todos os itens que o cluster contém e sua distribuição geral. ** \< ** Clique em um histograma quando **Legenda de Mineração** estiver visível e você puder ver os valores numéricos para cada  
  
 **Estados**  
 Esta coluna no gráfico é opcional e pode ser exibida ou removida selecionando a opção **Mostrar Legenda** . A coluna **Estados** fornece um guia sobre qual estado é representado por qual cor no histograma de clusters correspondente.  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Algoritmo de clustering de sequência da Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores de modelo de mineração de dados](data-mining/data-mining-model-viewers.md)   
 [Procurar um modelo usando o Visualizador de Cluster de Sequência da Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
