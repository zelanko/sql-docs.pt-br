---
description: CustomData (MDX)
title: CustomData (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ed7bfe2841caf9bd5b2c6e6caf102323db6d62ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413162"
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
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
