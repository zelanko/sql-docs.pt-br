---
title: Elemento DiagnosticInformation (ssbdiagnose) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssbdiagnose
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
caps.latest.revision: "14"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82593d8330e5f7263ff43c6b408998164425617f
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>Elemento DiagnosticInformation (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]O **DiagnosticInformation** elemento contém todos os elementos que reportam as informações de diagnósticas encontradas pelo utilitário. **DiagnosticInformation** é o elemento raiz de um arquivo de saída XML **ssbdiagnostic** .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo|Description|  
|---------------|-----------------|  
|**Nenhuma**|N/A|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhuma.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Uma vez por arquivo de saída XML **ssbdiagnose** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|Nenhuma.|  
|**Elementos filho**|[Elemento banner &#40; ssbdiagnose &#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)<br /><br /> [Elemento Issue &#40; ssbdiagnose &#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre namespaces XML, consulte [Namespaces em um documento XML](http://go.microsoft.com/fwlink/?LinkId=7341) na Biblioteca MSDN do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário ssbdiagnose &#40; O Service Broker &#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
