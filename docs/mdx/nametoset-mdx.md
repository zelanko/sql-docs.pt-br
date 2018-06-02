---
title: NameToSet (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 766049ff2c285de2b16e1aa67745a98eb22ef05f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580268"
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um conjunto que contém o membro especificado por uma cadeia de caracteres formatada em linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válida que representa o nome de um membro.  
  
## <a name="remarks"></a>Remarks  
 Se o nome do membro especificado existir, o **NameToSet** retorna um conjunto que contém esse membro. Caso contrário, a função retorna um conjunto vazio.  
  
> [!NOTE]  
>  O nome do membro especificado deve ser só um nome de membro; não pode ser uma expressão de membro. Para usar uma expressão de membro, consulte [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor de medida padrão para o nome de membro especificado.  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
