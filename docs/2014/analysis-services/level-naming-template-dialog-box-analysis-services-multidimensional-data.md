---
title: Caixa de diálogo modelo de nomeação de nível (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.levelnamingtemplatedialog.f1
helpviewer_keywords:
- Level Naming Template dialog box
ms.assetid: 96cad715-213e-4eac-9003-130a2f5fc985
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: febaae6051e8428d3fed2bb6533ce2c4d972950f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078055"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Modelo de Nomeação de Nível (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Modelo de Nomeação de Nível** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para construir o modelo de nomeação de nível para um atributo pai em uma dimensão. Para obter mais informações sobre modelos de nomeação de nível, consulte [Elemento NamingTemplate &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/namingtemplate-element-assl). Você pode exibir a caixa de diálogo **modelo de nomeação de nível** clicando no botão de reticências (**...**) no `NamingTemplate` valor de uma tradução para um atributo no painel **detalhes da conversão** na guia **traduções** do **Designer de dimensão**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Definir o modelo de nível**|Exibe uma grade na qual é possível projetar a hierarquia de níveis no atributo pai. A grade contém as seguintes colunas:<br /><br /> **Nível**: exibe a posição ordinal do nível para o qual o nome especificado em **nome** é usado. Para adicionar um novo modelo de nomeação para um nível, selecione **Nome** na linha que contém um asterisco (\*) em **Nível**.<br /><br /> **Nome**: contém o modelo de nomenclatura usado para o nível indicado em **nível**. Para adicionar um espaço reservado para a posição ordinal do nível no modelo de nomeação, adicione um único asterisco (*). Para adicionar um asterisco como parte do nome criado pelo modelo de nomeação, adicione dois asteriscos (\*\*).|  
|**Apagar tudo**|Selecione para remover todas as linhas em **Definir o modelo de nível**.|  
|**Disso**|Exibe o modelo de nomeação de nível construído pela caixa de diálogo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Traduções &#40;o designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
