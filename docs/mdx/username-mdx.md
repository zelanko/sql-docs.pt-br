---
title: UserName (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f8c08855d70d6a880607cc4310e6adcabbf7d9ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298028"
---
# <a name="username-mdx"></a>UserName (MDX)


  Retorna o nome de domínio e nome de usuário da conexão atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>Comentários  
 O valor retornado é uma cadeia de caracteres com o seguinte formato:  
  
 *nome de usuário de domínio*  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o nome de usuário do usuário que está executando a consulta.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
