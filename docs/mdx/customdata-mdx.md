---
title: CustomData (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5161bb180b6acdf8f6ab6d16d6d0f15bd8f40a39
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577808"
---
# <a name="customdata-mdx"></a>CustomData (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o valor da **CustomData** propriedade de cadeia de caracteres de conexão estiver definida; caso contrário, **nulo**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valor retornado  
 O **CustomData** função pode recuperar o **CustomData** propriedade de cadeia de conexão e transmitir uma configuração a ser usado por funções MDX (Multidimensional Expressions) e instruções, como [UserName (MDX)](../mdx/username-mdx.md) e [instrução CALL (MDX)](../mdx/mdx-data-manipulation-call.md). Por exemplo, essa função pode ser usada em uma expressão de segurança dinâmica para selecionar os membros do conjunto permitido/legado para o valor de cadeia de caracteres no **CustomData** propriedade de cadeia de caracteres de conexão.  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir exibe o valor retornado pelo **CustomData** função em uma medida calculada:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
