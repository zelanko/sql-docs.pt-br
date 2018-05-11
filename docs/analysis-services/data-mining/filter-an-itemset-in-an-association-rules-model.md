---
title: Filtro de modelo de regras de um conjunto de itens em uma associação | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cda9a614cbd5dc1e4863633bfadf07f3dc25e2ac
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="filter-an-itemset-in-an-association-rules-model"></a>Filtrar uma conjunto de itens em um modelo de regras de associação
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode filtrar os conjuntos de itens exibidos na guia **Conjuntos de Itens** do Visualizador de Regras de Associação do [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
### <a name="to-filter-an-itemset"></a>Para filtrar um conjunto de itens  
  
1.  Na guia **Visualizador do Modelos de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique na guia **Conjuntos de Itens** do **Visualizador de Regras de Associação**.  
  
2.  Insira uma condição de regra na caixa **Filtrar conjunto de itens** . Por exemplo, uma condição de regra poderia ser "Touring-1000 = existing"  
  
3.  Clique em **Inserir**.  
  
 Os conjuntos de itens são agora filtrados para exibir só os conjuntos de itens que contêm os itens selecionados. A caixa não diferencia maiúsculas de minúsculas. Os filtros são armazenados na memória para que você possa selecionar um filtro antigo da lista.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Visualizador do modelo e instruções de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
