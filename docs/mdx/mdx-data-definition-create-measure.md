---
description: Definição de dados MDX – CREATE MEASURE
title: Instrução CREATE MEASURE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cdbee6f6ede5e46926f1a8189792d86cf9e99f5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387262"
---
# <a name="mdx-data-definition---create-measure"></a>Definição de dados MDX – CREATE MEASURE


  Cria uma medida em um Modelo de Tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Table_Name*  
 Um literal de cadeia de caracteres válido que fornece o nome da tabela onde a medida será criada.  
  
 *Measure_Name*  
 Um literal de cadeia de caracteres válido que fornece um nome de medida.  
  
 *DAX_Expression*  
 Uma expressão DAX válida que retorna um único valor escalar.  
  
## <a name="remarks"></a>Comentários  
 O *MEASURE_NAME*  deve ser colocado entre parênteses.  
  
 A instrução CREATE MEASURE só pode ser usada dentro de uma definição de script MDX; consulte o [elemento MdxScript &#40;ASSL&#41;](https://docs.microsoft.com/analysis-services/assl/objects/mdxscript-element-assl?view=asallproducts-allversions).  
  
 Também é possível definir um membro calculado para ser usado por uma consulta única. Para definir um membro calculado limitado a uma consulta única, use a cláusula WITH na instrução SELECT. Para obter mais informações, consulte [Building Measures in MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-building-measures).  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
