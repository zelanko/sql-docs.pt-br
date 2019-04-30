---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91b4d64095c02fbf3f969248fc78d375a191fe72
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065254"
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
Especifica quais campos podem ser usados para detectar conflitos durante uma atualização otimista de uma linha da fonte de dados com um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
 Usar essas constantes com a **conjunto de registros** "**critérios de atualização**" propriedade dinâmica, que é referenciada no [índice de propriedade dinâmica do ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e documentadas no [ Microsoft Cursor Service para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|Detecta conflitos se qualquer coluna da linha de código-fonte de dados tiver sido alterada.|  
|**adCriteriaKey**|0|Detecta conflitos se a coluna de chave dos dados de linha de origem tiver sido alterada, que significa que a linha foi excluída.|  
|**adCriteriaTimeStamp**|3|Detecta conflitos se o carimbo de hora dos dados de linha de origem tiver sido alterada, que significa que a linha tiver sido acessada após o **Recordset** foi obtido.|  
|**adCriteriaUpdCols**|2|Detecta conflitos se qualquer uma das colunas da fonte de dados de linhas que correspondem aos campos atualizados dos **Recordset** foram alteradas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
