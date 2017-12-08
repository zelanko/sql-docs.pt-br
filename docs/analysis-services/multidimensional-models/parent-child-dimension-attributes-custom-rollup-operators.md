---
title: "Operadores de Rollup personalizados em dimensões pai-filho | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1d731ba3666e4569a45b6ab3e9254a1eaafdda35
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="parent-child-dimension-attributes---custom-rollup-operators"></a>Atributos de dimensão pai-filho - operadores de acúmulo personalizado
  Os operadores de acúmulo personalizado proporcionam uma maneira simples de controlar como os valores dos membros são acumulados nos valores pai em uma hierarquia pai-filho. Em uma dimensão que contém uma relação pai-filho, você especifica uma coluna que contém operadores unários que especificam o acúmulo para todos os membros não calculados do atributo pai. O operador unário é aplicado aos membros sempre que os valores dos membros pai são avaliados.  
  
 Os operadores unários são armazenados na coluna definida pela propriedade **UnaryOperatorColumn** do atributo pai e são aplicados a cada membro do atributo. A coluna especificada por essa propriedade pode residir na tabela de dimensões ou em uma tabela relacionada à tabela de dimensões por uma chave estrangeira desta.  
  
 Operadores de acúmulo personalizado oferecem funcionalidades semelhantes às das fórmulas de membro personalizado, porém mais simplificadas. Uma fórmula de membro personalizado utiliza expressões multidimensionais (MDX) para determinar como os membros são acumulados. Diferentemente, o operador de acúmulo personalizado emprega um operador unário simples para determinar como o valor de um membro afeta o pai. Fórmulas de membro personalizado do nível precedente em uma dimensão prevalecem sobre o operador de acúmulo personalizado do nível.  
  
## <a name="custom-rollup-precedence"></a>Precedência do acúmulo personalizado  
 Em termos de precedência, os operadores de acúmulo personalizado do atributo de origem para um nível da hierarquia prevalecem sobre as fórmulas de membro personalizado do nível anterior. No entanto, as fórmulas de membro personalizado do nível precedente prevalecem sobre os operadores de acúmulo personalizado de um nível.  
  
## <a name="see-also"></a>Consulte também  
 [Definir fórmulas de membro personalizado](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md)   
 [Operadores unários em dimensões pai-filho](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-unary-operators.md)  
  
  
