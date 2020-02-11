---
title: CustomData (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d2884e23cbee78acacdb72e386f0e99610e9629f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135833"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  Retorna o valor da propriedade de cadeia de conexão **CustomData** , se definido; caso contrário, **NULL**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valor retornado  
 A função **CustomData** pode recuperar a propriedade de cadeia de conexão **CustomData** e passar uma definição de configuração a ser usada por funções e instruções MDX (Multidimensional Expressions), como [nome de usuário (MDX)](../mdx/username-mdx.md) e [instrução de chamada (MDX)](../mdx/mdx-data-manipulation-call.md). Por exemplo, essa função pode ser usada em uma expressão de segurança dinâmica para selecionar os membros do conjunto permitido/negado para o valor da cadeia de caracteres na propriedade da cadeia de conexão **CustomData** .  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir exibe o valor retornado pela função **CustomData** em uma medida calculada:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
