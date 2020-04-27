---
title: Caixa de diálogo Definir relação (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.f1
helpviewer_keywords:
- Define Relationship dialog box
ms.assetid: 0fcee7f1-f138-4c2e-ae8c-245395ee0fe8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d80be1c4898ae00dfdbb88e22771c071636cf73c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082096"
---
# <a name="define-relationship-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Definir Relação (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Definir Relação** para definir uma relação entre uma dimensão de cubo e um grupo de medidas no Designer de Cubo. É possível exibir a caixa de diálogo **Definir Relação** clicando em **...** em uma célula no painel **Grade** na guia **Uso da Dimensão** no Designer de Cubo.  
  
## <a name="options"></a>Opções  
 **Selecionar tipo de relação**  
 Selecione o tipo de relação de dimensão a ser criada entre a dimensão de cubo e o grupo de medidas. A seleção de um tipo de relacionamento de dimensão altera o conteúdo do painel **Detalhes** .  
  
 Se **Nenhuma Relação** for escolhida, nenhuma relação de dimensão será criada.  
  
 **Detalhes**  
 Exibe as opções disponíveis para o tipo de relacionamento de dimensão selecionado em **Selecionar tipo de relação**.  
  
## <a name="detail-pane-options"></a>Opções do painel Detalhes  
 As seguintes opções são exibidas no painel **Detalhes** , dependendo do tipo de relacionamento selecionado em **Selecionar tipo de relação**:  
  
|Tipo de relação|Descrição|Opção|  
|-----------------------|-----------------|------------|  
|**Nenhuma Relação**|Nenhuma relação está definida e nenhuma opção é exibida no painel **Detalhes** .||  
|**Regular**|Especifica uma relação de dimensão normal. As seguintes opções são exibidas no painel **Detalhes** :|**Atributo de granularidade**: <br />                      Selecione o atributo que define a granularidade do grupo de medidas com relação à dimensão. Esse atributo normalmente é o atributo de chave da dimensão.|  
|||**Tabela de dimensões**: exibe a tabela principal da dimensão.|  
|||**Tabela de grupo de medidas**: exibe a tabela de fatos do grupo de medidas.|  
|||**Relação**: exibe uma grade de colunas de dimensão e colunas de grupos de medidas nas quais a relação é baseada. A grade contém as seguintes colunas:<br /><br /> **Colunas de dimensão**: exibe as colunas associadas ao atributo de granularidade selecionado. Observação: se a dimensão ainda não foi gerada, essa opção será definida como **Gerar**.<br />**Colunas de Grupos de Medidas** :<br />                              Selecione as colunas no grupo de medidas que estão relacionadas às colunas de dimensão.|  
|||**Avançado**:<br />                      Clique para exibir a caixa de diálogo **Associações de Grupos de Medidas** e edite as propriedades avançadas, como processamento nulo, em relações entre atributos e colunas de grupos de medidas. Para obter mais informações sobre a caixa de diálogo **associações de grupos de medidas** , consulte [caixa de diálogo associações de grupos de medidas &#40;Analysis Services-&#41;de dados multidimensionais ](measure-group-bindings-dialog-box-analysis-services-multidimensional-data.md).|  
|**Facto**|Especifica uma relação de dimensão de fato. As seguintes opções são exibidas no painel **Detalhes** :|**Atributo de granularidade**: selecione o atributo que define a granularidade do grupo de medidas com relação à dimensão. Esse atributo normalmente é o atributo de chave da dimensão.|  
|||**Tabela de dimensões**: exibe a tabela primária de dimensões.|  
|||**Tabela de grupos de medidas**: <br />                      Exibe a tabela na qual o grupo de medidas é baseado.|  
|**Referenciada**|Especifica uma relação de dimensão referenciada. As seguintes opções são exibidas no painel **Detalhes** :|**Dimensão de referência**: <br />                      Exibe a dimensão selecionada.|  
|||**Dimensão intermediária**: <br />                      Selecione a dimensão intermediária.|  
|||**Atributo de dimensão de referência**: <br />                      Selecione o atributo na dimensão de referência que está relacionado ao atributo da dimensão intermediária especificado em **Atributo de dimensão intermediária**.|  
|||**Atributo de dimensão intermediária**: <br />                      Selecione o atributo na dimensão intermediária que está relacionado ao atributo na dimensão de referência especificado em **Dimensão de referência**.|  
|||**Materialização**: <br />                      Selecione o armazenamento do membro do atributo na dimensão intermediária que vincula o atributo na dimensão de referência à tabela de fatos na estrutura MOLAP. A materialização da relação é o comportamento padrão para maximizar o desempenho das consultas, mas à custa de um aumento no tempo de processamento e do espaço de armazenamento.|  
|**Muitos para muitos**|Especifica uma relação de muitos para muitos da dimensão. As seguintes opções são exibidas no painel **Detalhes** :|**Dimensão** : exibe o tipo de dimensão selecionado.|  
|||**Grupo de medidas intermediário** : <br />                      Seleciona o grupo de medidas intermediário associado.<br /><br /> Observação: o grupo de medidas intermediário deve ter pelo menos uma dimensão em comum com o grupo de medidas selecionado. Além disso, a granularidade da relação entre o grupo de medidas intermediário e a dimensão comum deve ser maior ou igual à granularidade entre a dimensão comum e o grupo de medidas selecionado.|  
|**Mineração de dados**|Especifica uma relação de mineração de dados da dimensão. As seguintes opções são exibidas no painel **Detalhes** :|**Dimensão de destino**: exibe a dimensão de mineração de dados selecionada.<br /><br /> Observação: você deve selecionar uma dimensão de mineração de dados para criar uma relação de dimensão de mineração de dados.|  
|||**Dimensão de origem**: selecione a dimensão na qual a dimensão de mineração de dados fornece análise de previsão.|  
  
## <a name="see-also"></a>Consulte Também  
 [Relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Uso da dimensão &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
