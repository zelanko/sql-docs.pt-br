---
title: Caixa de diálogo associações de grupo de medidas (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.measuregroupbindings.f1
helpviewer_keywords:
- Measure Group Bindings dialog box
ms.assetid: ed642780-5350-438e-af73-b9ceab3f876d
author: minewiskan
ms.author: owend
ms.openlocfilehash: b4fb4b20fcccdabdf29aaf57dab65b1604a80a9e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541598"
---
# <a name="measure-group-bindings-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Associações de Grupos de Medidas (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Associações de Grupos de Medidas** para criar e modificar relações diretas entre atributos de não granularidade em uma dimensão de cubo e colunas em um grupo de medidas para uma relação de dimensão normal, bem como para especificar opções de processamento nulo para qualquer atributo em uma dimensão de cubo na caixa de diálogo **Definir Relação** .  
  
## <a name="options"></a>Opções  
 **Tabela de grupos de medidas**  
 Exibe o nome da tabela de fatos do grupo de medidas selecionado.  
  
 **Atributos**  
 Exibe uma grade de atributos e tabelas de dimensões. Selecione um atributo para criar ou modificar propriedades em **Relação** para o atributo selecionado. A grade contém as seguintes colunas:  
  
|Opção|Definição|  
|------------|----------------|  
|**Nome do atributo**|Exibe o nome do atributo.|  
|**Tabela de Dimensão**|Exibe o nome da tabela de dimensões na qual o atributo é baseado.|  
  
 **Relação**  
 Exibe uma grade de relações entre colunas da tabela de dimensões para o atributo selecionado e as colunas da tabela de fatos para o grupo de medidas selecionado, bem como a opção de processamento nulo da relação. A grade contém as seguintes colunas:  
  
|Opção|Definição|  
|------------|----------------|  
|**Colunas de Dimensão**|Exibe as colunas da tabela de dimensões na qual o atributo selecionado em **Atributos** é baseado.|  
|**Colunas de Grupos de Medidas**|Selecione a opção **Herdado da dimensão** para usar a relação do grupo de medidas herdada da dimensão ou selecione uma coluna da tabela de fatos na qual o grupo de medidas é baseado para definir uma relação explicitamente.|  
|**Processamento Nulo**|Selecione uma opção de processamento nulo para o atributo. Para obter mais informações sobre as opções de processamento nulo, consulte [Elemento NullProcessing &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl).|  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Definir relação &#40;Analysis Services-dados multidimensionais&#41;](define-relationship-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
