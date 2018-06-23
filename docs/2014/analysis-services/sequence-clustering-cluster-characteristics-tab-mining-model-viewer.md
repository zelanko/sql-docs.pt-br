---
title: Guia características do Cluster (Visualizador do modelo de mineração) msc | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.characteristics.f1
ms.assetid: 3a9e8a0c-7d03-47cc-8625-e68d73a8c947
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 75601cb33f04eaacfdb3970f858dd8a359abd4bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121576"
---
# <a name="sequence-clustering-cluster-characteristics-tab-mining-model-viewer"></a>Guia Características de Cluster do clustering de sequências (Visualizador do Modelo de Mineração)
  A guia **Características de Cluster** no **Visualizador de Clustering de Sequência da Microsoft** fornece uma lista detalhada das características que definem um cluster de sequência. Essas características podem incluir pares atributo-valor simples assim como podem fazer a transição entre estados.  
  
 Use esta exibição de um modelo de clustering de sequências para detalhar o conteúdo do cluster e ver as sequências que são representativas de um cluster.  
  
 **Para obter mais informações:** [Algoritmo MSC](data-mining/microsoft-sequence-clustering-algorithm.md), [Procurar um modelo usando o Visualizador de Cluster de Sequência da Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibir o que está presente na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador que será usado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado, ou o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Você também pode usar visualizadores de plug-in se houver.  
  
 **Cluster**  
 Escolha o cluster que você quer exibir.  
  
 **Características de \<Cluster >**  
 Esta tabela fornece uma lista das sequências que foram atribuídas ao cluster atual, ordenadas por probabilidade. Lembre-se de que uma sequência é basicamente um par atributo-valor, seguido por um ou mais pares atributo-valor adicionais. A combinação de sequências e as probabilidades são as características que definem cada cluster.  
  
 Por exemplo, em um modelo de clustering de sequência baseado em análise da cesta de compras, um cluster pode ter como sua principal característica um cliente escolhendo o item de venda e terminando a transação sem comprar nada mais. Em um modelo de clustering de sequência que procura analisar falhas de servidor, as características principais de um cluster podem ser uma série de eventos de erro de alta frequência.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Variável**|Esta coluna indica se a característica é um valor, ou uma transição.<br /><br /> Se a característica é um valor, o **variável** coluna contém o nome do atributo.<br /><br /> Se a característica representar uma transição de estado, o **variável** coluna contém o texto "Transições".|  
|**Valores**|O valor desta coluna depende se a característica é um par atributo-valor simples, ou uma transição de estado que representa uma sequência comum de itens ou eventos.<br /><br /> Se a característica é um valor, o **valor** coluna contém o estado.<br /><br /> Se a característica representar uma transição de estado, o **valor** coluna contém a descrição da transição de estado.|  
|**Probabilidade**|Esta coluna exibe uma barra que indica a probabilidade relativa que esta característica (um par atributo-valor simples ou uma combinação de estados) ser membro do cluster atual.<br /><br /> Você pode passar o mouse sobre o par para exibir o valor de frequência da característica.|  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – mineração de dados&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  