---
title: Contas de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d0dd0fabf7ebfc6ee020a533149b73e72f7a8a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126136"
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
|Elementos filho|[conta](../objects/account-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Dimensões, cujo [tipo](../properties/type-element-dimension-assl.md) é definido como *contas*, pode ter um atributo que especifica o tipo de conta, como renda, despesa e assim por diante, representado pelos membros da dimensão. O tipo de conta, em seguida, é usado pelo [medida](../objects/measure-element-assl.md) elementos, cujo [AggregationFunction](../properties/aggregatefunction-element-assl.md) é definido como *ByAccount*, para determinar a função de agregação a ser usado ao os membros da dimensão de agregação. O elemento `Accounts` contém uma coleção de elementos `Account`, que representam os tipos de conta e a função de agregação que deve ser usada para cada tipo de conta.  
  
 Um tipo de conta deve ser listado se a função de agregação for diferente do padrão usado pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para cada tipo de conta.  
  
 O conjunto de tipos de conta válidos é fixo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AccountCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento AccountType &#40;ASSL&#41;](../properties/accounttype-element-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
