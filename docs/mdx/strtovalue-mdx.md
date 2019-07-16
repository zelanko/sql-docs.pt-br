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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036694"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)


  Retorna o valor numérico especificado por uma cadeia de caracteres formatada para MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *MDX_Expression*  
 Uma expressão de cadeia de caracteres válida que resolve, direta ou indiretamente, uma célula única.  
  
## <a name="remarks"></a>Comentários  
 O **StrToValue** função retorna o valor numérico especificado pela expressão MDX. O **StrToValue** função normalmente é usada com funções definidas pelo usuário para retornar uma expressão MDX de uma função externa para uma instrução MDX que pode ser resolvida para uma única célula.  
  
-   Quando o sinalizador CONSTRAINED for usado, a expressão MDX deverá conter somente um valor de escalar. O sinalizador CONSTRAINED é usado para reduzir o risco de ataques de injeção pela cadeia de caracteres especificada. Se uma expressão MDX fornecida não for resolvida diretamente para um valor escalar, aparece o seguinte erro: "As restrições impostas pelo CONSTRAINED sinalizador na função STRTOVALUE foram violadas."  
  
-   Quando o sinalizador CONSTRAINED não for usado, a linguagem MDX especificada pode ser tão complexa quanto se desejar, desde que resolva a uma linguagem MDX válida que retorne uma célula única.  
  
> [!NOTE]  
>  Retornar o resultado de uma linguagem MDX como um valor numérico pode ser útil se o valor for armazenado como texto e você quiser executar operações aritméticas nos valores retornados.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa o **StrToValue** função para retornar o peso de cada bicicleta como um valor.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
