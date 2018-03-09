---
title: StrToValue (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: STRTOVALUE
dev_langs: kbMDX
helpviewer_keywords: StrToValue function
ms.assetid: 118a9c4f-74a3-48d5-a4f4-318664bc51bc
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 37424120aee0b38303b086019e2fb74a823cdc1b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
