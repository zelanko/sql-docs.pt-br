---
title: "Instrução REFRESH CUBE (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Cube
- REFRESH CUBE
- REFRESH_CUBE
- REFRESH
dev_langs: kbMDX
helpviewer_keywords:
- cubes [Analysis Services], cache
- refreshing cache
- REFRESH CUBE statement
- cache [Analysis Services]
ms.assetid: b8c087fb-5d17-4b13-b7cf-9929e9aab35c
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2656c588a90ce68f916815be28d157f1a51e0e23
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---refresh-cube"></a>Definição de dados MDX - atualização de cubo
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza o cache de cliente para um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de cubo.  
  
## <a name="remarks"></a>Comentários  
 Para aplicativos cliente conectados a uma instância de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], essa instrução faz com que a memória em cache no aplicativo cliente a ser sincronizado com o servidor. Enquanto isso será normalmente detectado e atualizado automaticamente, o período de tempo antes disso acontecer depende das configurações de cadeia de conexão do cliente. A instrução REFRESH CUBE atualiza os dados imediatamente.  
  
 Para os aplicativos cliente conectados a um cubo local, a instrução REFRESH CUBE faz com que o arquivo de cubo local seja recriado.  
  
> [!IMPORTANT]  
>  Os conjuntos nomeados armazenados no servidor não são atualizados.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de definição de dados MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
