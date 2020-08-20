---
description: Ordinal (MDX)
title: Ordinal (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 74811da22f8c73536749acad41dfbe859b00eeea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471728"
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)


  Retorna o valor ordinal com base em zero associado a um nível.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
## <a name="remarks"></a>Comentários  
 A função **ordinal** é frequentemente usada em conjunto com as funções **IIF** e **CurrentMember** para exibir condicionalmente valores diferentes em níveis de hierarquia diferentes, com base na posição ordinal de cada célula específica no resultado da consulta. Por exemplo, você pode usar a função **ordinal** para executar cálculos em determinados níveis e exibir um valor padrão de "N/a" em outros níveis.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o número ordinal para o nível Trimestre Calendário na hierarquia Calendário.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
