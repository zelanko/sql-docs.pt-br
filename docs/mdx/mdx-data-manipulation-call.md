---
title: Instrução CALL (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4052134e9fd7d3c6877894c61480897e40982b59
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741955"
---
# <a name="mdx-data-manipulation---call"></a>Manipulação de dados MDX - chamada


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
>  Se o procedimento armazenado não está registrado no cliente, o **chamar** instrução tenta chamar o procedimento armazenado de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de manipulação de dados MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Usando procedimentos armazenados &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
