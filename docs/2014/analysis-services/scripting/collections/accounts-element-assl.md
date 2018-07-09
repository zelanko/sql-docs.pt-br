---
title: Contas de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Accounts Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Accounts
helpviewer_keywords:
- Accounts element
ms.assetid: 3ec62f58-c19b-4b15-b040-8941521a389b
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 94e167c6eb804f3372fab6974403f0303f21a13a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277962"
---
# <a name="accounts-element-assl"></a>Elemento Accounts (ASSL)
  Contém a coleção de tipos de conta definidos em uma [banco de dados](../objects/database-element-assl.md) elemento.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum (coleção)|  
|Valor padrão|Nenhum (coleção)|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Banco de dados](../objects/database-element-assl.md)|  
|Elementos filho|[Conta](../objects/account-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Dimensões, cujo [tipo](../properties/type-element-dimension-assl.md) é definido como *contas*, pode ter um atributo que especifica o tipo de conta, como renda, despesa e assim por diante, representado pelos membros da dimensão. O tipo de conta, em seguida, é usado pelo [medida](../objects/measure-element-assl.md) elementos, cujo [AggregationFunction](../properties/aggregatefunction-element-assl.md) é definido como *ByAccount*, para determinar a função de agregação a ser usado ao os membros da dimensão de agregação. O elemento `Accounts` contém uma coleção de elementos `Account`, que representam os tipos de conta e a função de agregação que deve ser usada para cada tipo de conta.  
  
 Um tipo de conta deve ser listado se a função de agregação for diferente do padrão usado pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para cada tipo de conta.  
  
 O conjunto de tipos de conta válidos é fixo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AccountCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento AccountType &#40;ASSL&#41;](../properties/accounttype-element-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
