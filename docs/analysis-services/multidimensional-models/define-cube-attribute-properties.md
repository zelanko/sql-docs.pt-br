---
title: Definir propriedades de atributo de cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7e2ab2374955710452f1ba1cba91e3a4d8ff8c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025430"
---
# <a name="define-cube-attribute-properties"></a>Definir propriedades de atributo de cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  As propriedades de atributo de cubo permitem a especificação de configurações exclusivas para atributos de dimensão em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de um atributo de cubo.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**AggregationUsage**|Especifica como o Assistente de Design de Agregação projetará as agregações do atributo. O valor padrão é **Default**. Essa propriedade pode ter os seguintes valores:<br /><br /> **Default**:<br />                    O Assistente de Design de Agregação aplica uma regra padrão de acordo com o tipo de atributo (Completa para chaves, Irrestrita para as demais).<br /><br /> **None**:<br />                    Nenhuma agregação do cubo deve incluir esse atributo.<br /><br /> **Unrestricted**:<br />                    nenhuma restrição é imposta pelo Assistente de Design de Agregação<br /><br /> **Full**:<br />                    Toda agregação do cubo deve incluir esse atributo.|  
|**AttributeHierarchyEnabled**|Identifica se a hierarquia de atributo está ativa na dimensão do cubo. Possibilita desabilitar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente estiver desabilitada. O valor padrão é **True**.|  
|**OptimizedState**|Indica se a hierarquia de atributo foi otimizada na dimensão de cubo. Possibilita otimizar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente não estiver otimizada. O valor padrão é **FullyOptimized**. Essa propriedade pode ter os seguintes valores:<br /><br /> **FullyOptimized**: A instância cria índices para a hierarquia a fim de melhorar o desempenho das consultas. Este é o valor padrão.<br /><br /> **NotOptimized**:<br />                    A instância não cria índices adicionais.|  
|**AttributeHierarchyVisible**|Indica se a hierarquia de atributo está visível na dimensão de cubo. Possibilita visualizar hierarquias de atributo em cubos ou funções de dimensão específicos. Essa configuração não terá efeito se a hierarquia de atributo subjacente não estiver visível. O valor padrão é **True**.|  
|**AttributeID**|Contém o identificador exclusivo (ID) do atributo.|  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades de dimensão de cubo](../../analysis-services/multidimensional-models/define-cube-dimension-properties.md)   
 [Definir propriedades de hierarquia de cubo](../../analysis-services/multidimensional-models/define-cube-hierarchy-properties.md)  
  
  
