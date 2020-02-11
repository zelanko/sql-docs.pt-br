---
title: Elemento banner (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- banner element
- XML output file format [ssbdiagnose], banner element
- ssbdiagnose
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b2f425dd955e0c92daeaa0241e7ea01333222b75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63186873"
---
# <a name="banner-element-ssbdiagnose"></a>Elemento Banner (ssbdiagnose)
  Identifica qual utilitário gerou o arquivo XML de saída **ssbdiagnose** .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo|DESCRIÇÃO|  
|---------------|-----------------|  
|`title`|Identifica qual utilitário gerou o arquivo de saída XML **ssbdiagnose** .|  
|`product`|Identifica qual produto gerou o arquivo de saída XML **ssbdiagnose** .|  
|`version`|Identifica qual versão do utilitário gerou o arquivo de saída XML.|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|DESCRIÇÃO|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Ocorre uma vez por arquivo XML de saída **ssbdiagnose** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Este é um exemplo de um elemento Banner.  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  
