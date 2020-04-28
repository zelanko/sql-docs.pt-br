---
title: AddCalculatedMembers (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 982484b729b59a7106b6195e361110c1d4012653
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017177"
---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers (MDX)


  Retorna um conjunto gerado, adicionando membros calculados a um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 Por padrão, a linguagem MDX exclui membros calculados quando resolve funções de conjunto. A função **AddCalculatedMembers** examina a expressão de conjunto especificada em *Set_Expression* e inclui membros calculados que são irmãos dos membros contidos no escopo dessa expressão de conjunto.  
  
> [!NOTE]  
>  Essa função só pode ser usada com expressões de conjunto de uma dimensão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso dessa função.  
  
```  
-- This query returns the calculated members for the cube  
-- by retrieving all members, and then excluding non-calculated members.  
SELECT   
   AddCalculatedMembers(  
      {[Measures].Members}  
      )-[Measures].Members ON COLUMNS  
FROM [Adventure Works]   
```  
  
 O exemplo a seguir retorna `Measures.[Unit Price]` o membro, além de todos os membros calculados na dimensão de **medidas** , do cubo **Adventure Works** .  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
