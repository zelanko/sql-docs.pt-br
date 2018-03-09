---
title: Definir propriedades de atributo de cubo | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b87146458e6aee0cac066078f1d0dfb302f186d0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="define-cube-attribute-properties"></a>Definir propriedades de atributo de cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Propriedades de atributo de cubo permitem a especificação de configurações exclusivas para atributos de dimensão em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de um atributo de cubo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**AggregationUsage**|Especifica como o Assistente de Design de Agregação projetará as agregações do atributo. O valor padrão é **Default**. Essa propriedade pode ter os seguintes valores:<br /><br /> **Default**:<br />                    O Assistente de Design de Agregação aplica uma regra padrão de acordo com o tipo de atributo (Completa para chaves, Irrestrita para as demais).<br /><br /> **None**:<br />                    Nenhuma agregação do cubo deve incluir esse atributo.<br /><br /> **Unrestricted**:<br />                    nenhuma restrição é imposta pelo Assistente de Design de Agregação<br /><br /> **Full**:<br />                    Toda agregação do cubo deve incluir esse atributo.|  
|**AttributeHierarchyEnabled**|Identifica se a hierarquia de atributo está ativa na dimensão do cubo. Possibilita desabilitar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente estiver desabilitada. O valor padrão é **True**.|  
|**OptimizedState**|Indica se a hierarquia de atributo foi otimizada na dimensão de cubo. Possibilita otimizar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente não estiver otimizada. O valor padrão é **FullyOptimized**. Essa propriedade pode ter os seguintes valores:<br /><br /> **FullyOptimized**: a instância cria índices para a hierarquia a fim de melhorar o desempenho das consultas. Este é o valor padrão.<br /><br /> **NotOptimized**:<br />                    A instância não cria índices adicionais.|  
|**AttributeHierarchyVisible**|Indica se a hierarquia de atributo está visível na dimensão de cubo. Possibilita visualizar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente não estiver visível. O valor padrão é **True**.|  
|**AttributeID**|Contém o identificador exclusivo (ID) do atributo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Definir propriedades de dimensão de cubo](../../analysis-services/multidimensional-models/define-cube-dimension-properties.md)   
 [Definir propriedades de hierarquia de cubo](../../analysis-services/multidimensional-models/define-cube-hierarchy-properties.md)  
  
  
