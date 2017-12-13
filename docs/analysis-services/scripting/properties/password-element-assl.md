---
title: Elemento Password (ASSL) | Microsoft Docs
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
apiname: Password Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 29f5270c3fd7f427a469a6ac8513bf8f0b81e2d2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="password-element-assl"></a>Elemento Password (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a senha da conta de usuário para o [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor da **senha** elemento, bem como o valor da [conta](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md) elemento, será usado para fins de representação se o valor da [ImpersonationMode](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md) elemento para qualquer elemento derivado do **ImpersonationInfo** tipo de dados é definido como *ImpersonateAccount*.  
  
 Somente membros da função de administrador de servidor para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância pode fornecer um valor em branco para o **senha** elemento  
  
## <a name="see-also"></a>Consulte também  
 [Elemento DataSourceImpersonationInfo &#40; ASSL &#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
