---
title: Nome de usuário (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f1ebb5dc504b799575b2ccf9e47368e4e6511dac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097268"
---
# <a name="username-mdx"></a>UserName (MDX)


  Retorna o nome de domínio e nome de usuário da conexão atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>Comentários  
 O valor retornado é uma cadeia de caracteres com o seguinte formato:  
  
 *domain-name\user-name*  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o nome de usuário do usuário que está executando a consulta.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
