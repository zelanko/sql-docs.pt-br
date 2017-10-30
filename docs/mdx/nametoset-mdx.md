---
title: NameToSet (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NAMETOSET
dev_langs:
- kbMDX
helpviewer_keywords:
- NameToSet function
ms.assetid: e02e17d5-4309-49cb-84c7-5b445ac2bd94
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b615ddfdf8698e1d495e6d6070e489aa448d4c96
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="nametoset-mdx"></a>NameToSet (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto que contém o membro especificado por uma cadeia de caracteres formatada em linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válida que representa o nome de um membro.  
  
## <a name="remarks"></a>Comentários  
 Se o nome do membro especificado existir, o **NameToSet** retorna um conjunto que contém esse membro. Caso contrário, a função retorna um conjunto vazio.  
  
> [!NOTE]  
>  O nome do membro especificado deve ser só um nome de membro; não pode ser uma expressão de membro. Para usar uma expressão de membro, consulte [StrToSet &#40; MDX &#41; ](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor de medida padrão para o nome de membro especificado.  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

