---
title: Elemento BaseProperty (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f28d100ef59df6fe73b8dd93d1fbfebdb87bbb7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="baseproperty-element-csdlbi"></a>Elemento BaseProperty (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]O elemento BaseProperty é um tipo complexo que serve como base para outros elementos.  
  
 Seus atributos podem aparecer em colunas e em medidas.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento BaseProperty.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Alinhamento|não|O nome fornecido ao membro (coluna, medida, propriedade de navegação, hierarquia ou nível) que é definido pela implementação do tipo Member|  
|FormatString|não|O nome para exibição do membro.|  
|IsRightToLeft|não|Um valor booliano que indica se o campo contém texto que pode ser lido da direita para a esquerda.<br /><br /> Se esse atributo for omitido, será usada a configuração padrão (do modelo).|  
|SortDirection|não|Um valor que indica como os valores de campo geralmente são classificados. O conteúdo desse atributo é definido pelo tipo simples SortDirection.<br /><br /> Se esse atributo for omitido, será atribuída uma direção de classificação com base no tipo de dados do campo.|  
|Unidades|não|O símbolo que se aplica a valores de campos para expressar unidades.<br /><br /> Se ele for omitido, as unidades serão desconhecidas.|  
  
## <a name="alignment-element"></a>Elemento Alignment  
 Esse tipo simples define o formato de nomenclatura que é usado para resolver a ambiguidade de membros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Nenhum|Use o nome do atributo.|  
|Contexto|Use o nome da relação de entrada.|  
|Mesclagem|Concatene o nome da relação de entrada e o nome da propriedade, de acordo com as regras da gramática atual.|  
  
## <a name="sortdirection-element"></a>Elemento SortDirection  
 Esse tipo simples define o formato de nomenclatura que é usado para resolver a ambiguidade de membros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Nenhum|Use o nome do atributo.|  
|Contexto|Use o nome da relação de entrada.|  
|Mesclagem|Concatene o nome da relação de entrada e o nome da propriedade.|  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas sobre o modelo de objeto de tabela em compatibilidade 1050 1103 por meio de níveis](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
