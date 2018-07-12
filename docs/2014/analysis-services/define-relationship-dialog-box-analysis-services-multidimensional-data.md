---
title: Definir caixa de diálogo de relação (Analysis Services - dados multidimensionais) | Microsoft Docs
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
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.f1
helpviewer_keywords:
- Define Relationship dialog box
ms.assetid: 0fcee7f1-f138-4c2e-ae8c-245395ee0fe8
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93c76ad9d504e9ec6fc1ba417407a16bd93e8adf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165493"
---
# <a name="define-relationship-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Definir Relação (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Definir Relação** para definir uma relação entre uma dimensão de cubo e um grupo de medidas no Designer de Cubo. É possível exibir a caixa de diálogo **Definir Relação** clicando em **...** em uma célula no painel **Grade** na guia **Uso da Dimensão** no Designer de Cubo.  
  
## <a name="options"></a>Opções  
 **Selecionar tipo de relação**  
 Selecione o tipo de relação de dimensão a ser criada entre a dimensão de cubo e o grupo de medidas. A seleção de um tipo de relacionamento de dimensão altera o conteúdo do painel **Detalhes** .  
  
 Se **Nenhuma Relação** for escolhida, nenhuma relação de dimensão será criada.  
  
 **Detail**  
 Exibe as opções disponíveis para o tipo de relacionamento de dimensão selecionado em **Selecionar tipo de relação**.  
  
## <a name="detail-pane-options"></a>Opções do painel Detalhes  
 As seguintes opções são exibidas no painel **Detalhes** , dependendo do tipo de relacionamento selecionado em **Selecionar tipo de relação**:  
  
|Tipo de relação|Description|Opção|  
|-----------------------|-----------------|------------|  
|**Nenhuma relação**|Nenhuma relação está definida e nenhuma opção é exibida no painel **Detalhes** .||  
|**Regular**|Especifica uma relação de dimensão normal. As seguintes opções são exibidas no painel **Detalhes** :|**Atributo de granularidade**: <br />                      Selecione o atributo que define a granularidade do grupo de medidas com relação à dimensão. Esse atributo normalmente é o atributo de chave da dimensão.|  
|||**Tabela de dimensões**: exibe a tabela principal da dimensão.|  
|||**Tabela de grupo de medidas**: exibe a tabela de fatos do grupo de medidas.|  
|||**Relação**: exibe uma grade de colunas de dimensão e colunas de grupos de medidas nas quais a relação é baseada. A grade contém as seguintes colunas:<br /><br /> **Colunas de dimensão**: exibe as colunas associadas ao atributo de granularidade selecionado. Observação: se a dimensão ainda não foi gerada, essa opção será definida como **Gerar**.<br />**Colunas de Grupos de Medidas** :<br />                              Selecione as colunas no grupo de medidas que estão relacionadas às colunas de dimensão.|  
|||**Avançado**:<br />                      Clique para exibir a caixa de diálogo **Associações de Grupos de Medidas** e edite as propriedades avançadas, como processamento nulo, em relações entre atributos e colunas de grupos de medidas. Para obter mais informações sobre a caixa de diálogo **Associações de Grupos de Medidas**, consulte [Caixa de diálogo Associações de Grupos de Medidas &#40;Analysis Services – Dados Multidimensionais&#41;](measure-group-bindings-dialog-box-analysis-services-multidimensional-data.md).|  
|**Fato**|Especifica uma relação de dimensão de fato. As seguintes opções são exibidas no painel **Detalhes** :|**Atributo de granularidade**: selecione o atributo que define a granularidade do grupo de medidas com relação à dimensão. Esse atributo normalmente é o atributo de chave da dimensão.|  
|||**Tabela de dimensões**: exibe a tabela primária de dimensões.|  
|||**Tabela de grupos de medidas**: <br />                      Exibe a tabela na qual o grupo de medidas é baseado.|  
|**Referenciado**|Especifica uma relação de dimensão referenciada. As seguintes opções são exibidas no painel **Detalhes** :|**Dimensão de referência**: <br />                      Exibe a dimensão selecionada.|  
|||**Dimensão intermediária**: <br />                      Selecione a dimensão intermediária.|  
|||**Atributo de dimensão de referência**: <br />                      Selecione o atributo na dimensão de referência que está relacionado ao atributo da dimensão intermediária especificado em **Atributo de dimensão intermediária**.|  
|||**Atributo de dimensão intermediária**: <br />                      Selecione o atributo na dimensão intermediária que está relacionado ao atributo na dimensão de referência especificado em **Dimensão de referência**.|  
|||**Materializar**: <br />                      Selecione o armazenamento do membro do atributo na dimensão intermediária que vincula o atributo na dimensão de referência à tabela de fatos na estrutura MOLAP. A materialização da relação é o comportamento padrão para maximizar o desempenho das consultas, mas à custa de um aumento no tempo de processamento e do espaço de armazenamento.|  
|**Muitos-para-muitos**|Especifica uma relação de muitos para muitos da dimensão. As seguintes opções são exibidas no painel **Detalhes** :|**Dimensão** : exibe o tipo de dimensão selecionado.|  
|||**Grupo de medidas intermediário** : <br />                      Seleciona o grupo de medidas intermediário associado.<br /><br /> Observação: o grupo de medidas intermediário deve ter pelo menos uma dimensão em comum com o grupo de medidas selecionado. Além disso, a granularidade da relação entre o grupo de medidas intermediário e a dimensão comum deve ser maior ou igual à granularidade entre a dimensão comum e o grupo de medidas selecionado.|  
|**Mineração de Dados**|Especifica uma relação de mineração de dados da dimensão. As seguintes opções são exibidas no painel **Detalhes** :|**Dimensão de destino**: exibe a dimensão de mineração de dados selecionada.<br /><br /> Observação: você deve selecionar uma dimensão de mineração de dados para criar uma relação de dimensão de mineração de dados.|  
|||**Dimensão de origem**: selecione a dimensão na qual a dimensão de mineração de dados fornece análise de previsão.|  
  
## <a name="see-also"></a>Consulte também  
 [Relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Uso da dimensão &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
