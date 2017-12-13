---
title: Elemento Edition (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
apiname: Edition Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Edition
helpviewer_keywords: Edition element
ms.assetid: 521e1286-097e-494f-b036-61047096e87e
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6c1527f8f7af85fe2f258ec4c59a6c3749938016
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="edition-element-assl"></a>Elemento Edition (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a edição somente leitura da instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] representado pelo [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Server>  
      ...  
      <Edition>...</Edition>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Servidor](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **edição** elemento descreve qual edição do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] está instalado. O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Standard*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard edition para processadores de 32 bits.|  
|*Enterprise*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition para processadores de 32 bits.|  
|*EnterpriseCore*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition: licenciamento baseado em núcleo para processadores de 32 bits.|  
|*BusinessIntelligence*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Edição business Intelligence para processadores de 32 bits.|  
|*Desenvolvedor*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Developer edition para processadores de 32 bits|  
|*Avaliação*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Evaluation edition para processadores de 64 bits.|  
|*Local*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Local edition para processadores de 32 bits.|  
|*Standard64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard edition para processadores de 64 bits.|  
|*Enterprise64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition para processadores de 64 bits.|  
|*EnterpriseCore64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition: licenciamento baseado em núcleo para processadores de 64 bits.|  
|*BusinessIntelligence64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Edição business Intelligence para processadores de 64 bits.|  
|*Developer64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Developer edition para processadores de 64 bits|  
|*Evaluation64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Evaluation edition para processadores de 64 bits.|  
|*Local64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Local edition para processadores de 64 bits.|  
  
 A enumeração que corresponde aos valores permitidos para **edição do Server** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ServerEdition>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Version &#40; ASSL &#41;](../../../analysis-services/scripting/properties/version-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
