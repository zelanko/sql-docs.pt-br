---
title: Instrução CALL (MDX) | Microsoft Docs
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
- CALL
dev_langs:
- kbMDX
helpviewer_keywords:
- voids [MDX]
- stored procedures [MDX]
- CALL statement
ms.assetid: b534a20b-924c-43b8-832d-24e57d50425c
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6b3e7d095a7957c8d5af8dc497bb7a9d884005b8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-manipulation---call"></a>Manipulação de dados MDX - chamada
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 O **chamar** instrução executa um procedimento armazenado registrado especificado, incluindo, opcionalmente, um ou mais argumentos para o procedimento armazenado especificado. O **chamar** instrução é para uso apenas com procedimentos armazenados que retornam nulos. Essa instrução não pode ser combinada com outras funções nem operadores em uma linguagem MDX. Os procedimentos armazenados registrados que retornam valores podem ser chamados diretamente nas expressões MDX e combinados com outros operadores e funções MDX.  
  
 Se um cubo não for especificado, a instrução executará o procedimento armazenado no cubo atual.  
  
> [!NOTE]  
>  Se o procedimento armazenado não está registrado no cliente, o **chamar** instrução tenta chamar o procedimento armazenado de uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções MDX de manipulação de dados &#40; MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Usando procedimentos armazenados &#40; MDX &#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
