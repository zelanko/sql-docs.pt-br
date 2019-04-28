---
title: Caixa de diálogo (Analysis Services - dados multidimensionais) do modelo de nomeação de nível | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.levelnamingtemplatedialog.f1
helpviewer_keywords:
- Level Naming Template dialog box
ms.assetid: 96cad715-213e-4eac-9003-130a2f5fc985
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 37afa05887059607edc257c3957495a8db335d3c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728142"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Modelo de Nomeação de Nível (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Modelo de Nomeação de Nível** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para construir o modelo de nomeação de nível para um atributo pai em uma dimensão. Para obter mais informações sobre modelos de nomeação de nível, consulte [Elemento NamingTemplate &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/namingtemplate-element-assl). Você pode exibir o **modelo de nomeação de nível** caixa de diálogo clicando no botão de reticências (**...** ) na `NamingTemplate` o valor de uma tradução de um atributo no **detalhes de conversão** painel no **traduções** guia de **Designerdedimensão**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Definir o modelo de nível**|Exibe uma grade na qual é possível projetar a hierarquia de níveis no atributo pai. A grade contém as seguintes colunas:<br /><br /> **Nível**: Exibe a posição ordinal do nível para o qual o nome especificado em **Nome** é usado. Para adicionar um novo modelo de nomeação para um nível, selecione **Nome** na linha que contém um asterisco (\*) em **Nível**.<br /><br /> **Nome**: Contém o modelo de nomeação usado para o nível indicado em **Nível**. Para adicionar um espaço reservado para a posição ordinal do nível no modelo de nomeação, adicione um único asterisco (*). Para adicionar um asterisco como parte do nome criado pelo modelo de nomeação, adicione dois asteriscos (\*\*).|  
|**Limpar Tudo**|Selecione para remover todas as linhas em **Definir o modelo de nível**.|  
|**Resultado**|Exibe o modelo de nomeação de nível construído pela caixa de diálogo.|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Traduções &#40;Designer de dimensão&#41; &#40;Analysis Services - dados multidimensionais&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
