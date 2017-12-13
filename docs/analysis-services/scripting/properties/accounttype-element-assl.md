---
title: Elemento AccountType (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AccountType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AccountType
helpviewer_keywords: AccountType element
ms.assetid: 4fdf17d3-cd84-4bf6-9baf-21e15d4bf71e
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 66e550a87b6670106761f743eda1f4a6ada5eee7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="accounttype-element-assl"></a>Elemento AccountType (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o nome de um tipo de conta definido em um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
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
  
  
