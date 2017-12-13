---
title: Elemento ImpersonationInfoSecurity (ASSL) | Microsoft Docs
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
apiname: ImpersonationInfoSecurity Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ImpersonationInfoSecurity element
ms.assetid: 583fec36-90ef-4d6a-9888-ece6ae865c53
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8a36bde40a9229cf9c831323472d63dcf666b1ad
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="impersonationinfosecurity-element-assl"></a>Elemento ImpersonationInfoSecurity (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém um valor somente leitura que indica se foram feitas alterações de credenciais de segurança que são fornecidos no [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationInfoSecurity>...</ImpersonationInfoSecurity>  
  
</ImpersonationInfo>...  
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
|Elemento pai|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*PasswordRemoved*|As informações de senha foram removidas das credenciais de segurança fornecidas.|  
|*Inalterado*|Nenhuma alteração foi feita nas credenciais de segurança fornecidas.|  
  
 A enumeração que corresponde aos valores permitidos para **ImpersonationInfoSecurity** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ImpersonationInfoSecurity>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
