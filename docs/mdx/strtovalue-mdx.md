---
title: StrToValue (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1cf21e5b5dac57ce2d0c59e0ab82263727260792
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582288"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o valor numérico especificado por uma linguagem MDX – cadeia de caracteres formatada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *MDX_Expression*  
 Uma expressão de cadeia de caracteres válida que resolve, direta ou indiretamente, uma célula única.  
  
## <a name="remarks"></a>Remarks  
 O **StrToValue** função retorna o valor numérico especificado pela expressão MDX. O **StrToValue** função geralmente é usada com funções definidas pelo usuário para retornar uma expressão MDX de uma função externa para uma instrução MDX que pode ser resolvida para uma única célula.  
  
-   Quando o sinalizador CONSTRAINED for usado, a expressão MDX deverá conter somente um valor de escalar. O sinalizador CONSTRAINED é usado para reduzir o risco de ataques de injeção pela cadeia de caracteres especificada. Se uma linguagem MDX fornecida não for resolvida diretamente com um valor escalar; surge o seguinte erro: "As restrições impostas pelo sinalizador CONSTRAINED na função STRTOVALUE foram violadas."  
  
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
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
