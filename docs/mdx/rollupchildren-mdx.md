---
title: Função RollupChildren (MDX) | Microsoft Docs
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
- ROLLUPCHILDREN
dev_langs:
- kbMDX
helpviewer_keywords:
- RollupChildren function
ms.assetid: 6f092540-067d-443f-b631-8523836a0d86
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e3553458eecb094ec76ecb6bf7f65691aaa1c4bd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="rollupchildren-mdx"></a>Função RollupChildren (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 O **RollupChildren** função acumula os valores dos filhos do membro especificado usando o operador unário especificado.  
  
 A tabela a seguir descreve os operadores unários válidos para esta função.  
  
|Operador|Resultado|  
|--------------|------------|  
|**+**|total = total + filho atual|  
|**-**|total = total – filho atual|  
|**\***|total = total * filho atual|  
|**/**|total = total / filho atual|  
|**%**|total = (total / filho atual) * 100|  
|**~**|O filho não é usado no pacote cumulativo de atualizações. Seu valor é ignorado.|  
  
 Se o operador na propriedade do membro não aparecer na lista, um erro ocorrerá. A ordem de avaliação é determinada pela ordem dos irmãos, não pela prioridade dos operadores.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa uma propriedade do membro chamada “Operador de Acúmulo Alternativo” que contém valores alternativos para que os operadores unários acumulem filhos da hierarquia Lucro Líquido na dimensão Conta de uma maneira alternativa. Essa propriedade do membro não existe no cubo Adventure Works, mas poderia ser criada. Esse uso do **RollupChildren** função pode ser usada em um aplicativo de orçamento para análise hipotética.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
