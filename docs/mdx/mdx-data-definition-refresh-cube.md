---
title: Instrução de atualização de cubo (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 957609573c206b7c3492789c369d0fb2be2398a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038165"
---
# <a name="mdx-data-definition---refresh-cube"></a>Definição de dados MDX – REFRESH CUBE


  Atualiza o cache de cliente para um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de cubo.  
  
## <a name="remarks"></a>Comentários  
 Para aplicativos cliente conectados a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], essa instrução faz com que a memória armazenada em cache no aplicativo cliente seja sincronizada com o servidor. Enquanto isso será normalmente detectado e atualizado automaticamente, o período de tempo antes disso acontecer depende das configurações de cadeia de conexão do cliente. A instrução REFRESH CUBE atualiza os dados imediatamente.  
  
 Para os aplicativos cliente conectados a um cubo local, a instrução REFRESH CUBE faz com que o arquivo de cubo local seja recriado.  
  
> [!IMPORTANT]  
>  Os conjuntos nomeados armazenados no servidor não são atualizados.  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
