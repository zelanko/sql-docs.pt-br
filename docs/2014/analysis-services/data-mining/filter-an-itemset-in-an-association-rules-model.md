---
title: Filtrar um conjunto em um modelo de regras de associação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- filtering itemsets [Analysis Services]
- Mining Model Viewer [Analysis Services], itemsets
ms.assetid: 3ed919ea-8598-45d2-a4a0-b1b3357a4ab1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bef576a32bebc1c80b2ded8ee4831696811ba819
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084357"
---
# <a name="filter-an-itemset-in-an-association-rules-model"></a>Filtrar uma conjunto de itens em um modelo de regras de associação
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode filtrar os conjuntos de itens exibidos na guia **Conjuntos de Itens** do Visualizador de Regras de Associação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
### <a name="to-filter-an-itemset"></a>Para filtrar um conjunto de itens  
  
1.  Na guia **Visualizador do Modelos de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique na guia **Conjuntos de Itens** do **Visualizador de Regras de Associação**.  
  
2.  Insira uma condição de regra na caixa **Filtrar conjunto de itens** . Por exemplo, uma condição de regra poderia ser "Touring-1000 = existing"  
  
3.  Clique em **Inserir**.  
  
 Os conjuntos de itens são agora filtrados para exibir só os conjuntos de itens que contêm os itens selecionados. A caixa não diferencia maiúsculas de minúsculas. Os filtros são armazenados na memória para que você possa selecionar um filtro antigo da lista.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções do visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)  
  
  
