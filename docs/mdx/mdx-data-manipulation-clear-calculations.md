---
title: "Instrução CLEAR CALCULATIONS (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLEAR CALCULATIONS
- clalculations
- clear
dev_langs: kbMDX
helpviewer_keywords:
- clearing calculations
- CLEAR CALCULATIONS statement
- deleting calculations
- removing calculations
- calculations [Analysis Services], clearing
- cubes [Analysis Services], calculations
ms.assetid: aebec9a1-1d1d-4697-aa3f-cc2449625603
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ad7569a1db3d080c85dc0c45347c2dc011ee312d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-manipulation---clear-calculations"></a>Manipulação de dados MDX - CLEAR CALCULATIONS
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Remove todos os cálculos do cubo e retorna o cubo para a análise de cálculo 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Expression*  
 Uma expressão de cubo da linguagem MDX válida.  
  
## <a name="remarks"></a>Remarks  
 O **FROM** cláusula pode ser omitida quando o contexto do cubo é conhecido, como em um script MDX.  
  
> [!NOTE]  
>  Essa instrução só pode ser executada por um administrador de banco de dados ou servidor ou por um membro de uma função que tenha acesso aos dados de origem no cubo (ou seja, ReadSourceData=true)  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções MDX de manipulação de dados &#40; MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
