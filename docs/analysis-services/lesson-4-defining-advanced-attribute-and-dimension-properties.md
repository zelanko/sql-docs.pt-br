---
title: "Lição 4: Definindo avançado propriedades de dimensão e atributo | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0e86b9be-e47d-4bb4-87eb-136ff3a61aef
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: de9c7debe0b21d3f5d72a021f8bf6eb03bf7d06f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="lesson-4-defining-advanced-attribute-and-dimension-properties"></a>Lição 4: Definindo propriedades de dimensão e atributo avançadas
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Nesta lição, você aprenderá como usar algumas propriedades avançadas de atributos, hierarquias de atributo e propriedades de dimensão.  
  
> [!NOTE]  
> Esta lição baseia-se na versão aprimorada do projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você concluiu nas três primeiras lições deste tutorial. A primeira tarefa nesta lição descreve como localizar o projeto de exemplo apropriado que deve ser usado na lição e a diferença entre este projeto e o projeto que você criou nas três primeiras lições.  
  
Esta lição contém as seguintes tarefas:  
  
[Usando uma versão modificada do projeto do Tutorial do Analysis Services](../analysis-services/lesson-4-1-using-a-modified-version-of-the-analysis-services-tutorial-project.md)  
Nesta tarefa, você abrirá, revisará e implantará uma versão modificada do projeto Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , que contém vários grupos de medidas e dimensões adicionais.  
  
[Definindo propriedades de atributo pai em uma hierarquia pai-filho](../analysis-services/lesson-4-2-defining-parent-attribute-properties-in-a-parent-child-hierarchy.md)  
Nesta tarefa, você definirá nomes de nível em uma dimensão pai-filho e especificará se os dados relacionados aos membros pai serão exibidos. Para obter mais informações, consulte [Dimensões pai-filho](../analysis-services/multidimensional-models/parent-child-dimension.md) e [Atributos em hierarquias pai-filho](../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
[Agrupando membros de atributo automaticamente](../analysis-services/lesson-4-3-automatically-grouping-attribute-members.md)  
Nesta tarefa, você criará automaticamente agrupamento de membros de atributos com base na distribuição de membros dentro da hierarquia de atributos. Para obter mais informações, consulte [Agrupar membros de atributo &#40;Diferenciação&#41;](../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
[Ocultando e desabilitando as hierarquias de atributo](../analysis-services/lesson-4-4-hiding-and-disabling-attribute-hierarchies.md)  
Nesta tarefa, você aprenderá como e quando desativar ou ocultar as hierarquias de atributo.  
  
[Classificando membros de atributo com base em um atributo secundário](../analysis-services/lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)  
Nesta tarefa, você aprenderá como classificar os membros de dimensão com base em um atributo secundário para atingir a ordem de classificação desejada.  
  
[Especificando relações de atributos entre atributos em uma hierarquia definida pelo usuário](../analysis-services/4-6-specifying-attribute-relationships-in-user-defined-hierarchy.md)  
Nesta tarefa, você aprenderá a definir propriedades de membro para atributos e especificar relações de agregação entre eles. Para obter mais informações, consulte [Definir relações de atributo](../analysis-services/multidimensional-models/attribute-relationships-define.md) e [Propriedades da hierarquia de usuário](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md).  
  
[Definindo o membro desconhecido e as propriedades de processamento nulo](../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
Nesta tarefa, você configura as propriedades UnknownMember e UnknownMemberName para tratar as condições de erro causadas por membros de dimensão nulos.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 5: Definindo relações entre grupos de medidas e dimensões](../analysis-services/lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)  
  
## <a name="see-also"></a>Consulte também  
[Cenário do tutorial de Analysis Services](../analysis-services/analysis-services-tutorial-scenario.md)  
[Modelagem multidimensional &#40; Tutorial do Adventure Works &#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
[Dimensões em modelos multidimensionais](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
  
