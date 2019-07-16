---
title: Função RollupChildren (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 89f7545af0d98de2a6bd97630a893057aac36b12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037052"
---
# <a name="rollupchildren-mdx"></a>Função RollupChildren (MDX)


  Retorna um valor gerado pelo acúmulo dos valores dos filhos de um membro especificado usando o operador unário especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Unary_Operator*  
 Uma expressão de cadeia de caracteres válida que especifica um operador unário.  
  
## <a name="remarks"></a>Comentários  
 O **RollupChildren** função acumula os valores dos filhos do membro especificado usando o operador unário especificado.  
  
 A tabela a seguir descreve os operadores unários válidos para esta função.  
  
|Operador|Resultado|  
|--------------|------------|  
|**+**|total = total + filho atual|  
|**-**|total = total – filho atual|  
|**\***|total = total * filho atual|  
|**/**|total = total / filho atual|  
|**%**|total = (total / filho atual) * 100|  
|**~**|O filho não é usado no acúmulo. Seu valor é ignorado.|  
  
 Se o operador na propriedade do membro não aparecer na lista, um erro ocorrerá. A ordem de avaliação é determinada pela ordem dos irmãos, não pela prioridade dos operadores.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa uma propriedade do membro chamada “Operador de Acúmulo Alternativo” que contém valores alternativos para que os operadores unários acumulem filhos da hierarquia Lucro Líquido na dimensão Conta de uma maneira alternativa. Essa propriedade do membro não existe no cubo Adventure Works, mas poderia ser criada. Esse uso do **RollupChildren** função poderia ser usada em um aplicativo de orçamento para análise hipotética.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
