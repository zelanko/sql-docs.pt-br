---
title: Nametoset=1=«nome (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d42a94ce4e878a3f4ac0ef14a48872bf5d32a144
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542456"
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)


  Retorna um conjunto que contém o membro especificado por uma cadeia de caracteres formatada para MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válida que representa o nome de um membro.  
  
## <a name="remarks"></a>Comentários  
 Se o nome do membro especificado existir, o **NameToSet** função retorna um conjunto que contém aquele membro. Caso contrário, a função retorna um conjunto vazio.  
  
> [!NOTE]  
>  O nome do membro especificado deve ser só um nome de membro; não pode ser uma expressão de membro. Para usar uma expressão de membro, consulte [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor de medida padrão para o nome de membro especificado.  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
