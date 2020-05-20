---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: rothja
ms.author: jroth
ms.openlocfilehash: ecdc80a2f1e1ace36170a9b4527ba01f0b02ee11
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760652"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Para um objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) do RDS, especifica a prioridade de execução do thread assíncrono que recupera dados.  
  
 Use essas constantes com a propriedade dinâmica "**prioridade de thread em segundo plano**" do **conjunto de registros** , que é referenciada no índice de propriedade dinâmica do ADO para OLE DB e documentada no [serviço de cursor da Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Define a prioridade entre normal e mais alta.|  
|**adPriorityBelowNormal**|2|Define a prioridade entre a mais baixa e a normal.|  
|**adPriorityHighest**|5|Define a prioridade para o mais alto possível.|  
|**AdPriorityLowest**|1|Define a prioridade para o mais baixo possível.|  
|**adPriorityNormal**|3|Define a prioridade como normal.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. AdcPropAsyncThreadPriority. ABOVENORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. BELOWNORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. mais alto|  
|AdoEnums. AdcPropAsyncThreadPriority. mais baixo|  
|AdoEnums. AdcPropAsyncThreadPriority. NORMAL|
