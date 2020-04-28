---
title: StrToValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cad8fec605a56a60cfcc7024739225e474fd42f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036694"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)


  Retorna o valor numérico especificado por uma cadeia de caracteres formatada com MDX (Multidimensional Expressions).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *MDX_Expression*  
 Uma expressão de cadeia de caracteres válida que resolve, direta ou indiretamente, uma célula única.  
  
## <a name="remarks"></a>Comentários  
 A função **StrToValue** retorna o valor numérico especificado pela expressão MDX. A função **StrToValue** normalmente é usada com funções definidas pelo usuário para retornar uma expressão MDX de uma função externa de volta para uma instrução MDX que pode ser resolvida para uma única célula.  
  
-   Quando o sinalizador CONSTRAINED for usado, a expressão MDX deverá conter somente um valor de escalar. O sinalizador CONSTRAINED é usado para reduzir o risco de ataques de injeção pela cadeia de caracteres especificada. Se uma linguagem MDX fornecida não for resolvida diretamente com um valor escalar; surge o seguinte erro: "As restrições impostas pelo sinalizador CONSTRAINED na função STRTOVALUE foram violadas."  
  
-   Quando o sinalizador CONSTRAINED não for usado, a linguagem MDX especificada pode ser tão complexa quanto se desejar, desde que resolva a uma linguagem MDX válida que retorne uma célula única.  
  
> [!NOTE]  
>  Retornar o resultado de uma linguagem MDX como um valor numérico pode ser útil se o valor for armazenado como texto e você quiser executar operações aritméticas nos valores retornados.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a função **StrToValue** para retornar o peso de cada bicicleta como um valor.  
  
```  
WITH MEMBER Measures.x AS   
StrToValue   
   ([Product].[Product].CurrentMember.Properties ('Weight')  
   ,CONSTRAINED  
   )  
SELECT Measures.x ON 0  
,[Product].[Product].[Product].Members ON 1  
FROM [Adventure Works]  
WHERE [Product].[Product Categories].[Bikes]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
