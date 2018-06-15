---
title: Contas de elemento (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bf3d3b56e9cc2b299ddcdec1c0a506e0168f8741
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030497"
---
# <a name="accounts-element-assl"></a>Elemento Accounts (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém a coleção de tipos de conta que são definidos em um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database>  
   ...  
   <Accounts>  
      <Account>...</Account>  
   </Accounts>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum (coleção)|  
|Valor padrão|Nenhum (coleção)|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Elementos filho|[Conta](../../../analysis-services/scripting/objects/account-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Dimensões, cujo [tipo](../../../analysis-services/scripting/properties/type-element-dimension-assl.md) é definido como *contas*, pode ter um atributo que especifica o tipo de conta, como renda, despesa e assim por diante, representado pelos membros da dimensão. O tipo de conta é usado por [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md) elementos, cujo [AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md) é definido como *ByAccount*, para determinar a função de agregação a ser usado ao os membros da dimensão de agregação. O elemento **Accounts** contém uma coleção de elementos **Account** , que representam os tipos de conta e a função de agregação que deve ser usada para cada tipo de conta.  
  
 Um tipo de conta deve ser listado se a função de agregação for diferente do padrão usado pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para cada tipo de conta.  
  
 O conjunto de tipos de conta válidos é fixo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AccountCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento AccountType &#40;ASSL&#41;](../../../analysis-services/scripting/properties/accounttype-element-assl.md)   
 [Coleções de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
