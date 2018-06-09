---
title: Instrução REFRESH CUBE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dafc13dda1f8ecab1400a88d1ca66eff5f317e43
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741725"
---
# <a name="mdx-data-definition---refresh-cube"></a>Definição de dados MDX - atualização de cubo


  Atualiza o cache de cliente para um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de cubo.  
  
## <a name="remarks"></a>Remarks  
 Para aplicativos cliente conectados a uma instância de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], essa instrução faz com que a memória em cache no aplicativo cliente a ser sincronizado com o servidor. Enquanto isso será normalmente detectado e atualizado automaticamente, o período de tempo antes disso acontecer depende das configurações de cadeia de conexão do cliente. A instrução REFRESH CUBE atualiza os dados imediatamente.  
  
 Para os aplicativos cliente conectados a um cubo local, a instrução REFRESH CUBE faz com que o arquivo de cubo local seja recriado.  
  
> [!IMPORTANT]  
>  Os conjuntos nomeados armazenados no servidor não são atualizados.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
