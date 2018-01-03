---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords: ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8a03809de8f86cf4ece91be598a71cd24b3ad9d7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Para um RDS [registros](../../../ado/reference/ado-api/recordset-object-ado.md) de objeto, especifica a prioridade de execução do thread assíncrono que recupera dados.  
  
 Usar essas constantes com o **registros** "**prioridade de Thread em segundo plano**" propriedade dinâmica, que é referenciada no índice de propriedade dinâmica de banco de dados ADO para OLE e documentada no [ Serviço de Cursor da Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentação.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Define a prioridade entre normais e maior.|  
|**adPriorityBelowNormal**|2|Define a prioridade entre menor e normal.|  
|**adPriorityHighest**|5|Define a prioridade para o mais alto possível.|  
|**AdPriorityLowest**|1|Define a prioridade para o nível mais baixo possível.|  
|**adPriorityNormal**|3|Define a prioridade normal.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
