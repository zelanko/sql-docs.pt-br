---
description: FilterGroupEnum
title: FilterGroupEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
author: rothja
ms.author: jroth
ms.openlocfilehash: f8d3c510cfd9fa6c4a28f78005021465b9b0917b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443658"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
Especifica o grupo de registros a ser filtrado de um [conjunto](../../../ado/reference/ado-api/recordset-object-ado.md)de registros.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|Filtros para exibir somente os registros afetados pela última chamada de [exclusão](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [ressincronização](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) .|  
|**adFilterConflictingRecords**|5|Filtros para exibir os registros que falharam na última atualização do lote.|  
|**adFilterFetchedRecords**|3|Filtros para exibir os registros no cache atual – ou seja, os resultados da última chamada para recuperar registros do banco de dados.|  
|**adFilterNone**|0|Remove o filtro atual e restaura todos os registros para exibição.|  
|**adFilterPendingRecords**|1|Filtros para exibir somente os registros que foram alterados, mas que ainda não foram enviados ao servidor. Aplicável somente para o modo de atualização do lote.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. FilterMode. AFFECTEDRECORDS|  
|AdoEnums. FilterMode. CONFLICTINGRECORDS|  
|AdoEnums. FilterMode. FETCHEDRECORDS|  
|AdoEnums. FilterMode. NONE|  
|AdoEnums. FilterMode. PENDINGRECORDS|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade Filter](../../../ado/reference/ado-api/filter-property.md)
