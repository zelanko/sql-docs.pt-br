---
title: Elemento AccountType (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e07561d0cd4272c202786f931fdd0dbc3c4eda8d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="accounttype-element-assl"></a>Elemento AccountType (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Receita*|A conta é uma conta de receita.|  
|*Despesa*|A conta é uma conta de despesa.|  
|*Fluxo*|A conta é uma conta de fluxo de caixa.|  
|*Saldo*|A conta é uma conta de saldo.|  
|*Ativo*|A conta é uma conta de ativos.|  
|*Dívida*|A conta é uma conta de passivos.|  
|*Estatística*|A conta é uma conta estatística.|  
  
 A enumeração que corresponde aos valores permitidos para **AccountType** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AccountTypes>.  
  
## <a name="see-also"></a>Consulte também  
 [Contas de elemento &#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
