---
title: Elemento DiagnosticInformation (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 55da8efd6ee5b330e259ed78bdd152720403f310
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186906"
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>Elemento DiagnosticInformation (ssbdiagnose)
  O elemento **DiagnosticInformation** contém todos os elementos que reportam as informações de diagnóstico encontradas pelo utilitário. **DiagnosticInformation** é o elemento raiz de um arquivo de saída XML **ssbdiagnostic** .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|attribute|Descrição|  
|---------------|-----------------|  
|`None`|N/D|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Uma vez por arquivo de saída XML **ssbdiagnose** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|Nenhum.|  
|**Elementos filho**|[Elemento Banner &#40;ssbdiagnose&#41;](banner-element-ssbdiagnose.md)<br /><br /> [Elemento Issue &#40;ssbdiagnose&#41;](issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre namespaces XML, consulte [Namespaces em um documento XML](https://go.microsoft.com/fwlink/?LinkId=7341) na Biblioteca MSDN do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  
