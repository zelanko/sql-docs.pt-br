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
ms.openlocfilehash: e4b0a858c3e87aa657f02d106f6e6db453ee0cb0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088326"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Modelo de Nomeação de Nível (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Modelo de Nomeação de Nível** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para construir o modelo de nomeação de nível para um atributo pai em uma dimensão. Para obter mais informações sobre modelos de nomeação de nível, consulte [Elemento NamingTemplate &#40;ASSL&#41;](scripting/properties/namingtemplate-element-assl.md). Você pode exibir o **modelo de nomeação de nível** caixa de diálogo clicando no botão de reticências (**...** ) na `NamingTemplate` o valor de uma tradução de um atributo no **detalhes de conversão** painel no **traduções** guia de **Designerdedimensão**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Definir o modelo de nível**|Exibe uma grade na qual é possível projetar a hierarquia de níveis no atributo pai. A grade contém as seguintes colunas:<br /><br /> **Nível**: exibe a posição ordinal do nível para o qual o nome especificado no **nome** é usado. Para adicionar um novo modelo de nomeação para um nível, selecione **Nome** na linha que contém um asterisco (\*) em **Nível**.<br /><br /> **Nome da**: contém o modelo de nomeação usado para o nível indicado na **nível**. Para adicionar um espaço reservado para a posição ordinal do nível no modelo de nomeação, adicione um único asterisco (*). Para adicionar um asterisco como parte do nome criado pelo modelo de nomeação, adicione dois asteriscos (\*\*).|  
|**Limpar Tudo**|Selecione para remover todas as linhas em **Definir o modelo de nível**.|  
|**Resultado**|Exibe o modelo de nomeação de nível construído pela caixa de diálogo.|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Traduções &#40;Designer de dimensão&#41; &#40;Analysis Services - dados multidimensionais&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
