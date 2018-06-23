---
title: Operadores de Rollup personalizados em dimensões pai-filho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ac668355cf3886c904ad8a1757020fac3c10a12d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118758"
---
# <a name="custom-rollup-operators-in-parent-child-dimensions"></a>Operadores de rollup personalizados em dimensões pai-filho
  Os operadores de acúmulo personalizado proporcionam uma maneira simples de controlar como os valores dos membros são acumulados nos valores pai em uma hierarquia pai-filho. Em uma dimensão que contém uma relação pai-filho, você especifica uma coluna que contém operadores unários que especificam o acúmulo para todos os membros não calculados do atributo pai. O operador unário é aplicado aos membros sempre que os valores dos membros pai são avaliados.  
  
 Os operadores unários são armazenados na coluna definida pela propriedade `UnaryOperatorColumn` do atributo pai e são aplicados a cada membro do atributo. A coluna especificada por essa propriedade pode residir na tabela de dimensões ou em uma tabela relacionada à tabela de dimensões por uma chave estrangeira desta.  
  
 Operadores de acúmulo personalizado oferecem funcionalidades semelhantes às das fórmulas de membro personalizado, porém mais simplificadas. Uma fórmula de membro personalizado utiliza expressões multidimensionais (MDX) para determinar como os membros são acumulados. Diferentemente, o operador de acúmulo personalizado emprega um operador unário simples para determinar como o valor de um membro afeta o pai. Fórmulas de membro personalizado do nível precedente em uma dimensão prevalecem sobre o operador de acúmulo personalizado do nível.  
  
## <a name="custom-rollup-precedence"></a>Precedência do acúmulo personalizado  
 Em termos de precedência, os operadores de acúmulo personalizado do atributo de origem para um nível da hierarquia prevalecem sobre as fórmulas de membro personalizado do nível anterior. No entanto, as fórmulas de membro personalizado do nível precedente prevalecem sobre os operadores de acúmulo personalizado de um nível.  
  
## <a name="see-also"></a>Consulte também  
 [Definir fórmulas de membro personalizado](attribute-properties-define-custom-member-formulas.md)   
 [Operadores unários em dimensões pai-filho](parent-child-dimension-attributes-unary-operators.md)  
  
  