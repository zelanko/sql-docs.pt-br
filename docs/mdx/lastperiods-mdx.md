---
title: LastPeriods (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 102382bf2acc2300d5862b48c5341c218e785275
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578978"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um conjunto de membros até e inclusive um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Index*  
 Uma expressão numérica válida que especifica vários períodos.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 Se o número especificado de períodos for positivo, o **LastPeriods** retorna um conjunto de membros que começa com o membro defasagem *índice* -1 da expressão de membro especificado e termina com o membro especificado. O número de membros retornados pela função é igual a *índice*.  
  
 Se o número especificado de períodos for negativo, o **LastPeriods** função retorna um conjunto de membros que começa com o membro especificado e termina com o membro que lidera (- *índice* - 1) do membro especificado. O número de membros retornados pela função é igual ao valor absoluto do *índice*.  
  
 Se o número especificado de períodos for zero, o **LastPeriods** função retorna o conjunto vazio. Isso é diferente de **latência** função, que retorna o membro especificado se 0 for especificado.  
  
 Se um membro não for especificado, o **LastPeriods** função usa **Time.CurrentMember**. Se nenhuma dimensão for marcada como uma dimensão Tempo, a função será analisada e executada sem um erro, mas causará um erro de célula no aplicativo cliente.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o valor de medida padrão durante o segundo, terceiro e quarto trimestres fiscais do ano fiscal 2002.  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Esse exemplo também pode ser escrito usando o operador : (dois-pontos):  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 O exemplo a seguir retorna o valor de medida padrão durante o primeiro trimestre fiscal do ano fiscal 2002. Embora o número especificado de períodos seja três, apenas um pode ser retornado porque não há períodos anteriores no ano fiscal.  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
