---
title: "Função KPIWeight (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: KPIWeight function
ms.assetid: 6d585c76-b4c4-437f-8433-cfa4e6057af1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 06f1c5e8a1ed26355f2fbe71f00e9f7b2125248b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="kpiweight-mdx"></a>Função KPIWeight (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o peso do KPI (indicador chave de desempenho) especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
KPIWeight(KPI_Name)  
```  
  
## <a name="arguments"></a>Argumentos  
 *KPI_Name*  
 Uma expressão de cadeia de caracteres válida que especifica o nome do KPI.  
  
## <a name="remarks"></a>Comentários  
 O valor retornado é a contribuição do KPI ao pai.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
