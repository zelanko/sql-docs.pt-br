---
title: Elemento AccountType (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname:
- AccountType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AccountType
helpviewer_keywords:
- AccountType element
ms.assetid: 4fdf17d3-cd84-4bf6-9baf-21e15d4bf71e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cdb339861e5b12a9f020af51fe96847fe8ca9b36
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="accounttype-element-assl"></a>Elemento AccountType (ASSL)
  Contém o nome de um tipo de conta definido em um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Account>  
   ...  
   <AccountType>...</AccountType>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Conta](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Lucros e perdas*|A conta é uma conta de receita.|  
|*Despesas*|A conta é uma conta de despesa.|  
|*Fluxo*|A conta é uma conta de fluxo de caixa.|  
|*Saldo*|A conta é uma conta de saldo.|  
|*Ativo*|A conta é uma conta de ativos.|  
|*Responsabilidade*|A conta é uma conta de passivos.|  
|*Estatística*|A conta é uma conta estatística.|  
  
 A enumeração que corresponde aos valores permitidos para **AccountType** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AccountTypes>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Accounts &#40; ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

