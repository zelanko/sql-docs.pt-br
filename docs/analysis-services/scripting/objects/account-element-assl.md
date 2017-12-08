---
title: Conta de elemento (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Account Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Account
helpviewer_keywords: Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: efe72ade8623910c34a1aff1d5439ee707c27f7b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="account-element-assl"></a>Elemento Account (ASSL)
  Contém detalhes sobre um tipo de conta dentro de um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Accounts>  
   <Account>  
      <AccountType>...</AccountType>  
      <AggregationFunction>...</AggregationFunction>  
            <Aliases>...</Aliases>  
            <Annotations>...</Annotations>  
   </Account>  
</Accounts>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Contas](../../../analysis-services/scripting/collections/accounts-element-assl.md)|  
|Elementos filho|[AccountType](../../../analysis-services/scripting/properties/accounttype-element-assl.md), [AggregationFunction](../../../analysis-services/scripting/properties/aggregationfunction-element-assl.md), [Aliases](../../../analysis-services/scripting/collections/aliases-element-assl.md), [anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Dimensões, cujo [tipo](../../../analysis-services/scripting/properties/type-element-dimension-assl.md) é definido como *contas,* pode ter um atributo que especifica o tipo de conta, como renda, despesa e assim por diante, representado pelos membros da dimensão. O tipo de conta é usado por [medidas](../../../analysis-services/scripting/objects/measure-element-assl.md) elementos, cujo [AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md) é definido como *ByAccount*, para determinar a função de agregação a ser usado ao os membros da dimensão de agregação. O elemento **Account** representa um único tipo de conta e a função de agregação que deveriam ser usados por tais medidas.  
  
 Um tipo de conta deve ser listado se a função de agregação for diferente do padrão usado pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para cada tipo de conta.  
  
 O conjunto de tipos de conta válidos é fixo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Account>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de banco de dados &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
