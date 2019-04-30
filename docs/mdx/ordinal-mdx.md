---
title: Ordinal (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 83036ec2ee0fa69c9ebb8cc2a905361eeae0aafa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278115"
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
 O **Ordinal** função frequentemente é usada em conjunto com o **IIF** e **CurrentMember** funções para exibir valores diferentes condicionalmente em diferentes níveis de hierarquia, com base na posição ordinal de cada célula específica no resultado da consulta. Por exemplo, você pode usar o **Ordinal** função para executar cálculos em determinados níveis e exibir um valor padrão de "N/d" em outros níveis.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o número ordinal para o nível Trimestre Calendário na hierarquia Calendário.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
