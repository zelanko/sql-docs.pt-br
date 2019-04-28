---
title: Definir propriedades de atributo de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e84c49055a1fdb5b11487ab17af19762f86686c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726410"
---
# <a name="define-cube-attribute-properties"></a>Definir propriedades de atributo de cubo
  As propriedades de atributo de cubo permitem a especificação de configurações exclusivas para atributos de dimensão em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de um atributo de cubo.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`AggregationUsage`|Especifica como o Assistente de Design de Agregação projetará as agregações do atributo. Essa propriedade pode ter os seguintes valores:<br /><br /> `Default`: Padrão. O Assistente de Design de Agregação aplica uma regra padrão de acordo com o tipo de atributo (Completa para chaves, Irrestrita para as demais).<br /><br /> `None`: Nenhuma agregação do cubo deve incluir esse atributo.<br /><br /> `Unrestricted`: Nenhuma restrição é imposta no Assistente de Design de agregação.<br /><br /> `Full`: Toda agregação do cubo deve incluir esse atributo.|  
|`AttributeHierarchyEnabled`|Identifica se a hierarquia de atributo está ativa na dimensão do cubo. Possibilita desabilitar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente estiver desabilitada. O valor padrão é `True`.|  
|`OptimizedState`|Indica se a hierarquia de atributo foi otimizada na dimensão de cubo. Possibilita otimizar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente não estiver otimizada. Essa propriedade pode ter os seguintes valores:<br /><br /> `FullyOptimized`: Padrão. A instância cria índices para a hierarquia a fim de melhorar o desempenho das consultas. Este é o valor padrão.<br /><br /> `NotOptimized`: A instância não cria índices adicionais.|  
|`AttributeHierarchyVisible`|Indica se a hierarquia de atributo está visível na dimensão de cubo. Possibilita visualizar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente não estiver visível. O valor padrão é `True`.|  
|`AttributeID`|Contém o identificador exclusivo (ID) do atributo.|  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades de dimensão de cubo](define-cube-dimension-properties.md)   
 [Definir propriedades de hierarquia de cubo](define-cube-hierarchy-properties.md)  
  
  
