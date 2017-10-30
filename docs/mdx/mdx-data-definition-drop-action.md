---
title: "Instrução DROP ACTION (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP
- DROP ACTION
- Action
- DROP_ACTION
dev_langs:
- kbMDX
helpviewer_keywords:
- DROP ACTION statement
- deleting actions
- removing actions
- actions [MDX]
- dropping actions
ms.assetid: 74b3cfee-dea8-4968-a54c-1754d52ee1bd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99866db174208e4d041e69cae3d3b520eefb8dba
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---drop-action"></a>Definição de dados MDX - ação de SOLTAR
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui uma ação especificada de um cubo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome do cubo.  
  
 *Action_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome da ação que está sendo descartada.  
  
## <a name="see-also"></a>Consulte também  
 [Criar ação instrução &#40; MDX &#41;](../mdx/mdx-data-definition-create-action.md)   
 [Instruções de definição de dados MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

