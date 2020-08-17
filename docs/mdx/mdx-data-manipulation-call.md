---
description: Manipulação de dados MDX – CALL
title: Instrução CALL (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a8f3b550e3fed3fe28e74896c3c4ff764db8810
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387031"
---
# <a name="mdx-data-manipulation---call"></a>Manipulação de dados MDX – CALL


  Executa um procedimento armazenado que retorna um nulo no escopo atual ou opcionalmente em um cubo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SP_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome de um procedimento armazenado.  
  
 *SP_Argument*  
 Uma expressão de cadeia de caracteres válida que fornece um argumento ao procedimento armazenado chamado.  
  
 *Cube_Expression*  
 Uma expressão de cubo de cadeia de caracteres válida que fornece o nome do cubo.  
  
## <a name="remarks"></a>Comentários  
 A instrução **Call** executa um procedimento armazenado registrado especificado, incluindo, opcionalmente, um ou mais argumentos para o procedimento armazenado especificado. A instrução **Call** é para uso somente com procedimentos armazenados que retornam voids. Essa instrução não pode ser combinada com outras funções nem operadores em uma linguagem MDX. Os procedimentos armazenados registrados que retornam valores podem ser chamados diretamente nas expressões MDX e combinados com outros operadores e funções MDX.  
  
 Se um cubo não for especificado, a instrução executará o procedimento armazenado no cubo atual.  
  
> [!NOTE]  
>  Se o procedimento armazenado não estiver registrado no cliente, a instrução **Call** tentará chamar o procedimento armazenado de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de manipulação de dados MDX &#40;&#41;MDX ](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Usando procedimentos armazenados &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
