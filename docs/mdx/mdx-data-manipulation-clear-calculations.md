---
title: "Instrução CLEAR CALCULATIONS (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
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
ms.openlocfilehash: 12302161e25d184e3fcffb2ee9d32636208d13a0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-manipulation---clear-calculations"></a>Manipulação de dados MDX - CLEAR CALCULATIONS
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove todos os cálculos do cubo e retorna o cubo para a análise de cálculo 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Expression*  
 Uma expressão de cubo da linguagem MDX válida.  
  
## <a name="remarks"></a>Comentários  
 O **FROM** cláusula pode ser omitida quando o contexto do cubo é conhecido, como em um script MDX.  
  
> [!NOTE]  
>  Essa instrução só pode ser executada por um administrador de banco de dados ou servidor ou por um membro de uma função que tenha acesso aos dados de origem no cubo (ou seja, ReadSourceData=true)  
  
## <a name="see-also"></a>Consulte também  
 [Instruções MDX de manipulação de dados &#40; MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
