---
title: "Operadores de rollup personalizados em dimens&#245;es pai-filho | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "operações de acúmulo filho"
  - "propriedade UnaryOperatorColumn"
  - "operadores rollup personalizado [Analysis Services]"
  - "operadores unários"
  - "dimensões pai-filho [Analysis Services]"
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Operadores de rollup personalizados em dimens&#245;es pai-filho
  Os operadores de acúmulo personalizado proporcionam uma maneira simples de controlar como os valores dos membros são acumulados nos valores pai em uma hierarquia pai-filho. Em uma dimensão que contém uma relação pai-filho, você especifica uma coluna que contém operadores unários que especificam o acúmulo para todos os membros não calculados do atributo pai. O operador unário é aplicado aos membros sempre que os valores dos membros pai são avaliados.  
  
 Os operadores unários são armazenados na coluna definida pela propriedade **UnaryOperatorColumn** do atributo pai e são aplicados a cada membro do atributo. A coluna especificada por essa propriedade pode residir na tabela de dimensões ou em uma tabela relacionada à tabela de dimensões por uma chave estrangeira desta.  
  
 Operadores de acúmulo personalizado oferecem funcionalidades semelhantes às das fórmulas de membro personalizado, porém mais simplificadas. Uma fórmula de membro personalizado utiliza expressões multidimensionais (MDX) para determinar como os membros são acumulados. Diferentemente, o operador de acúmulo personalizado emprega um operador unário simples para determinar como o valor de um membro afeta o pai. Fórmulas de membro personalizado do nível precedente em uma dimensão prevalecem sobre o operador de acúmulo personalizado do nível.  
  
## Precedência do acúmulo personalizado  
 Em termos de precedência, os operadores de acúmulo personalizado do atributo de origem para um nível da hierarquia prevalecem sobre as fórmulas de membro personalizado do nível anterior. No entanto, as fórmulas de membro personalizado do nível precedente prevalecem sobre os operadores de acúmulo personalizado de um nível.  
  
## Consulte também  
 [Definir fórmulas de membro personalizado](../../analysis-services/multidimensional-models/define-custom-member-formulas.md)   
 [Operadores unários em dimensões pai-filho](../../analysis-services/multidimensional-models/unary-operators-in-parent-child-dimensions.md)  
  
  