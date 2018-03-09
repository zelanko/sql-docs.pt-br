---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf0c00fb7f353171686f57405879b3beb544aa1d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
Especifica quais campos podem ser usados para detectar conflitos durante uma atualização otimista de uma linha da fonte de dados com um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
 Usar essas constantes com o **Recordset** "**critérios de atualização**" propriedade dinâmica, que é referenciada no [índice de propriedade dinâmica de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e documentado no [ Serviço de Cursor da Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentação.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|Detecta os conflitos se qualquer coluna da linha de fonte de dados tiver sido alterada.|  
|**adCriteriaKey**|0|Detecta conflitos se a coluna de chave de dados de linha de origem foi alterada, o que significa que a linha foi excluída.|  
|**adCriteriaTimeStamp**|3|Detecta conflitos se o carimbo de hora dos dados de linha de origem foi alterada, o que significa que a linha tiver sido acessada após o **registros** foi obtido.|  
|**adCriteriaUpdCols**|2|Detecta conflitos se qualquer uma das colunas da fonte de dados de linhas que correspondem aos campos atualizados o **registros** foram alteradas.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC Equivalent  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
