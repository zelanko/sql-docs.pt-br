---
description: Função Error (MDX)
title: Erro (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f95ee71586f5571d91221fe8889198a44a1252b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494919"
---
# <a name="error-mdx"></a>Função Error (MDX)


  Identifica um erro, fornecendo uma mensagem de erro específica (opcional).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Error_Text*  
 Uma expressão de cadeia de caracteres válida que contém a mensagem de erro a ser retornada.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra como usar a função **Error** dentro de uma medida calculada:  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
