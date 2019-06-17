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
manager: kfile
ms.openlocfilehash: 172915d99b231490cbdca24f70d1d38da27a1d3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248323"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  Retorna o valor da **CustomData** propriedade de cadeia de caracteres de conexão estiver definida; caso contrário, **nulo**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valor retornado  
 O **CustomData** função possa recuperar o **CustomData** propriedade de cadeia de conexão e transmitir uma configuração a ser usado por funções MDX (Multidimensional Expressions) e instruções, como [UserName (MDX)](../mdx/username-mdx.md) e [instrução CALL (MDX)](../mdx/mdx-data-manipulation-call.md). Por exemplo, essa função pode ser usada em uma expressão de segurança dinâmica para selecionar os membros do conjunto permitido/negado para o valor de cadeia de caracteres na **CustomData** propriedade de cadeia de caracteres de conexão.  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir exibe o valor retornado pela **CustomData** função em uma medida calculada:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
