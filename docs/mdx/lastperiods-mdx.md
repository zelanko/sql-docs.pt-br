---
title: LastPeriods (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6a9337e925da40f148bbe0d2c77fb1cf4f5f1a99
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905772"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)


  Retorna um conjunto de membros até e inclusive um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Índice*  
 Uma expressão numérica válida que especifica vários períodos.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Se o número especificado de períodos for positivo, a função **LastPeriods** retornará um conjunto de membros que começam com o membro que atrasa o *índice* -1 da expressão de membro especificada e termina com o membro especificado. O número de membros retornados pela função é igual ao *índice*.  
  
 Se o número especificado de períodos for negativo, a função **LastPeriods** retornará um conjunto de membros que começam com o membro especificado e termina com o membro que leva (- *index* -1) do membro especificado. O número de membros retornados pela função é igual ao valor absoluto do *índice*.  
  
 Se o número especificado de períodos for zero, a função **LastPeriods** retornará o conjunto vazio. Isso é diferente da função **lag** , que retorna o membro especificado se 0 for especificado.  
  
 Se um membro não for especificado, a função **LastPeriods** usará **time. CurrentMember**. Se nenhuma dimensão for marcada como uma dimensão Tempo, a função será analisada e executada sem um erro, mas causará um erro de célula no aplicativo cliente.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
