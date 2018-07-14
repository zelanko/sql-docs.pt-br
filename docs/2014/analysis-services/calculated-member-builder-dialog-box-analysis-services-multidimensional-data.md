---
title: Calculado (Analysis Services - dados multidimensionais) da caixa de diálogo do construtor de membro | Microsoft Docs
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
- sql12.asvs.calculatedmemberbuilderdialog.f1
ms.assetid: 73b89a9f-f403-4ab8-99f7-e3ceb870c260
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b2df3f9bdb11a344d332a50580a992680118afa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220496"
---
# <a name="calculated-member-builder-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Construtor de Membro Calculado (Analysis Services - Dados multidimensionais)
  Use a caixa de diálogo **Construtor de Membro Calculado** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar um membro calculado.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome**|Digite o nome do membro calculado.|  
|**Hierarquia pai**|Selecione a hierarquia na qual o membro calculado será criado.|  
|**Membro pai**|Essa opção estará habilitada se você selecionar uma hierarquia pai (diferente do `Measures` dimensão) que tem mais de um nível. Clique no botão de reticências (**…**) para selecionar um membro pai. O membro pai determina o local do membro calculado na estrutura de dimensão.|  
|**Expression**|Digite a expressão MDX que será usada.|  
|**Verificar**|Clique em **Verificar** para testar a expressão MDX definida em **Expressão**.|  
|**Metadados**|Exibe metadados para o objeto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] atual que pode ser incluído na expressão MDX definida em **Expressão**.<br /><br /> É possível copiar a sintaxe MDX do item selecionado clicando com o botão direito do mouse no item e selecionando **Copiar**ou arrastando o item selecionado para **Expressão**.|  
|**Funções**|Exibe as funções MDX disponíveis para a instância atual do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Os itens listados são recuperados do conjunto de linhas do esquema MDSCHEMA_FUNCTIONS.<br /><br /> É possível copiar a sintaxe MDX do item selecionado clicando com o botão direito do mouse no item e selecionando **Copiar**ou arrastando o item selecionado para **Expressão**.|  
  
## <a name="see-also"></a>Consulte também  
 [Expressões multidimensionais &#40;MDX&#41; referência](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
