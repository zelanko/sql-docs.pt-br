---
title: Filtro de um conjunto de itens em uma associação de modelo de regras | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- filtering itemsets [Analysis Services]
- Mining Model Viewer [Analysis Services], itemsets
ms.assetid: 3ed919ea-8598-45d2-a4a0-b1b3357a4ab1
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 150575298dd25b282af845303e3e4ae206888d1b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185373"
---
# <a name="filter-an-itemset-in-an-association-rules-model"></a>Filtrar uma conjunto de itens em um modelo de regras de associação
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode filtrar os conjuntos de itens exibidos na guia **Conjuntos de Itens** do Visualizador de Regras de Associação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
### <a name="to-filter-an-itemset"></a>Para filtrar um conjunto de itens  
  
1.  Na guia **Visualizador do Modelos de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique na guia **Conjuntos de Itens** do **Visualizador de Regras de Associação**.  
  
2.  Insira uma condição de regra na caixa **Filtrar conjunto de itens** . Por exemplo, uma condição de regra poderia ser "Touring-1000 = existing"  
  
3.  Clique em **Inserir**.  
  
 Os conjuntos de itens são agora filtrados para exibir só os conjuntos de itens que contêm os itens selecionados. A caixa não diferencia maiúsculas de minúsculas. Os filtros são armazenados na memória para que você possa selecionar um filtro antigo da lista.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)  
  
  
