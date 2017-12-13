---
title: Elemento ImpersonationMode (ASSL) | Microsoft Docs
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
apiname: ImpersonationMode Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ImpersonateMode
helpviewer_keywords: ImpersonateMode element
ms.assetid: 160fdcb2-ac9f-4c5a-a0eb-a5f7669166b9
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 38db9801572f444c5316546c3737bfa15181b6d1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="impersonationmode-element-assl"></a>Elemento ImpersonationMode (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém um valor que indica o método de representação para elementos que são derivados do [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationMode>...</ImpersonationMode>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Default*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Default*|O pai usa o método de representação mais adequado para o contexto no qual a representação é usada.|  
|*ImpersonateAccount*|O pai usa as credenciais da conta de usuário que é especificada no elemento pai.|  
|*ImpersonateAnonymous*|O pai usa as credenciais de um usuário anônimo.|  
|*ImpersonateCurrentUser*|O pai usa as credenciais do usuário atual.|  
|*ImpersonateServiceAccount*|O pai usa as credenciais da conta de serviço que está associado com a instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
 A enumeração que corresponde aos valores permitidos para **ImpersonationMode** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ImpersonationLevel>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
