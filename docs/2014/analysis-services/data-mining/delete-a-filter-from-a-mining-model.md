---
title: Excluir um filtro de um modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- filters [Analysis Services]
ms.assetid: 91220b21-adbc-49a9-b200-8bf0a724eff1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a8b19c9c23857013796885eb8d2d3469607eae17
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084726"
---
# <a name="delete-a-filter-from-a-mining-model"></a>Excluir um filtro de um modelo de mineração
  Quando você cria um filtro em um modelo de mineração, pode criar modelos em um subconjunto dos dados na exibição da fonte de dados. Os filtros também são úteis para testar a precisão do modelo em um subconjunto dos dados originais.  
  
 Porém, você deve excluir o filtro se quiser exibir novamente o conjunto completo de casos. Este procedimento descreve como remover as condições em um filtro ou excluir completamente o filtro.  
  
### <a name="to-delete-a-condition-from-a-filter-on-a-mining-model"></a>Para excluir uma condição de um filtro em um modelo de mineração  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no Gerenciador de Soluções, clique na estrutura de mineração que contém o modelo de mineração a filtrar.  
  
2.  Clique na guia **Modelos de Mineração** .  
  
3.  Selecione o modelo, e clique com o botão direito do mouse para abrir o menu de atalho.  
  
     -ou-  
  
     Selecione o modelo. No menu **Modelo de Mineração** , selecione **Definir Filtro de Modelos**.  
  
4.  Na caixa de diálogo **Filtro de Modelos** , clique com o botão direito do mouse na linha da grade que contém a condição a excluir.  
  
5.  Selecione **Excluir**.  
  
### <a name="to-clear-the-filter-on-a-mining-model-in-the-filter-editor-dialog-box"></a>Para desmarcar o filtro em um modelo de mineração na caixa de diálogo Editor de Filtro  
  
-   Na caixa de diálogo **Editor de Filtro** , clique com o botão direito do mouse em uma linha na grade e selecione **Excluir Tudo**.  
  
## <a name="working-with-model-filters-using-the-properties-window"></a>Trabalhando com os filtros de modelos usando a janela Propriedades  
 Para excluir o filtro inteiro, você não precisa abrir as caixas de diálogo do editor de filtro. As condições de filtro que você criou estão disponíveis na propriedade `Filter` do modelo de mineração.  
  
> [!NOTE]  
>  Você pode exibir as propriedades de um modelo de mineração no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], mas não no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-clear-the-filter-on-a-mining-model-in-solution-explorer"></a>Para desmarcar o filtro em um modelo de mineração no Gerenciador de Soluções  
  
1.  No Gerenciador de Soluções, clique no modelo de mineração que contém o filtro.  
  
2.  Na janela **Propriedades** , clique com o botão direito do mouse no texto `Filter` do filtro na propriedade e selecione **selecionar tudo**.  
  
3.  Pressione a tecla Backspace ou Delete.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhar os dados de caso de um modelo de mineração](drill-through-to-case-data-from-a-mining-model.md)   
 [Tarefas e instruções do modelo de mineração](mining-model-tasks-and-how-tos.md)   
 [Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-models-analysis-services-data-mining.md)  
  
  
