---
title: Instrução CREATE MEASURE (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: f264ba96-cbbe-488b-8ac9-b3056a6e997b
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 8868863d2bba43ba8f9a0fff9f9f2aa5f5331bc4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---create-measure"></a>Definição de dados MDX - criar medidas
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 O *Measure_Name* devem ser colocados entre colchetes.  
  
 A instrução CREATE MEASURE somente pode ser usada dentro de uma definição de script MDX; consulte [elemento MdxScript &#40;ASSL&#41;](../analysis-services/scripting/objects/mdxscript-element-assl.md).  
  
 Também é possível definir um membro calculado para ser usado por uma consulta única. Para definir um membro calculado limitado a uma consulta única, use a cláusula WITH na instrução SELECT. Para obter mais informações, consulte [compilando medidas em MDX](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
