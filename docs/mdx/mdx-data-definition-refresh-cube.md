---
title: Instrução REFRESH CUBE (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Cube
- REFRESH CUBE
- REFRESH_CUBE
- REFRESH
dev_langs:
- kbMDX
helpviewer_keywords:
- cubes [Analysis Services], cache
- refreshing cache
- REFRESH CUBE statement
- cache [Analysis Services]
ms.assetid: b8c087fb-5d17-4b13-b7cf-9929e9aab35c
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 37649d37d1cef67eb50caf8f3768beba19545988
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-definition---refresh-cube"></a>Definição de dados MDX - atualização de cubo
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Atualiza o cache de cliente para um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de cubo.  
  
## <a name="remarks"></a>Remarks  
 Para aplicativos cliente conectados a uma instância de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], essa instrução faz com que a memória em cache no aplicativo cliente a ser sincronizado com o servidor. Enquanto isso será normalmente detectado e atualizado automaticamente, o período de tempo antes disso acontecer depende das configurações de cadeia de conexão do cliente. A instrução REFRESH CUBE atualiza os dados imediatamente.  
  
 Para os aplicativos cliente conectados a um cubo local, a instrução REFRESH CUBE faz com que o arquivo de cubo local seja recriado.  
  
> [!IMPORTANT]  
>  Os conjuntos nomeados armazenados no servidor não são atualizados.  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de definição de dados MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
