---
title: KPIStatus (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c0824a9235aa7fd949910800d1e8ce20eab709e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63272898"
---
# <a name="kpistatus-mdx"></a>KPIStatus (MDX)


  Retorna um valor normalizado que representa a porção de status do KPI (indicador chave de desempenho) especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
KPIStatus(KPI_Name)  
```  
  
## <a name="arguments"></a>Argumentos  
 *KPI_Name*  
 Uma expressão de cadeia de caracteres válida que especifica o nome do KPI.  
  
## <a name="remarks"></a>Comentários  
 O valor de status geralmente é um valor normalizado entre -1 e 1.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor de KPI, o objetivo de KPI, o status de KPI e a tendência de KPI para a medida de renda por canal para os descendentes de três membros da hierarquia do atributo Ano fiscal:  
  
```  
SELECT  
   { KPIValue("Channel Revenue"),   
     KPIGoal("Channel Revenue"),  
     KPIStatus("Channel Revenue"),   
     KPITrend("Channel Revenue")  
   } ON Columns,  
Descendants  
   ( { [Date].[Fiscal].[Fiscal Year].&[2002],  
       [Date].[Fiscal].[Fiscal Year].&[2003],  
       [Date].[Fiscal].[Fiscal Year].&[2004]   
     }, [Date].[Fiscal].[Fiscal Quarter]  
   ) ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
