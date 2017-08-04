---
title: Membros (String) (MDX) | Microsoft Docs
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
- Members
dev_langs:
- kbMDX
helpviewer_keywords:
- Members function
ms.assetid: 21fca354-448b-4b05-93f4-111bde1568f1
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 14ab54616fdfeb85cb5b45f1e6d77b8e5c475c41
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="members-string-mdx"></a>Membros (cadeia de caracteres) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um membro especificado por uma expressão de cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válida que especifica um nome de membro.  
  
## <a name="remarks"></a>Comentários  
 O **membros (cadeia de caracteres)** função retorna um membro único cujo nome é especificado. Normalmente, você usa o **membros (cadeia de caracteres)** função com funções externas, fornecendo ao **membros (cadeia de caracteres)** uma cadeia de caracteres que identifica um membro de função e o **membros (cadeia de caracteres)** função retorna o valor para o membro especificado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa o **membros (cadeia de caracteres)** para converter a cadeia de caracteres especificada em um membro válido de função e, em seguida, retorna a medida padrão para o membro especificado na cadeia de caracteres. A cadeia de caracteres especificada está entre aspas simples. A medida padrão é a medida Valor das Vendas do Revendedor.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

