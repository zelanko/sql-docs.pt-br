---
title: CustomData (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EXISTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Exists function
ms.assetid: 61d9f5a2-6f56-4179-a39b-317c8e0a2cdd
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5fb7c745ac65b41095c3d4dfb41b62b081d83c1d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="customdata-mdx"></a>CustomData (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o valor da **CustomData** propriedade de cadeia de caracteres de conexão estiver definida; caso contrário, **nulo**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 O **CustomData** função pode recuperar o **CustomData** propriedade de cadeia de conexão e transmitir uma configuração a ser usado por funções MDX (Multidimensional Expressions) e instruções, como [UserName (MDX)](../mdx/username-mdx.md) e [instrução CALL (MDX)](../mdx/mdx-data-manipulation-call.md). Por exemplo, essa função pode ser usada em uma expressão de segurança dinâmica para selecionar os membros do conjunto permitido/legado para o valor de cadeia de caracteres no **CustomData** propriedade de cadeia de caracteres de conexão.  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir exibe o valor retornado pelo **CustomData** função em uma medida calculada:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
