---
title: RecordStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
author: rothja
ms.author: jroth
ms.openlocfilehash: f84f43a90479064c2a95d407b7f816fd48c1c679
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756760"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
Especifica o [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) de um registro em relação às atualizações em lotes e outras operações em massa.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|Indica que o registro não foi salvo porque a operação foi cancelada.|  
|**adRecCantRelease**|0x400|Indica que o novo registro não foi salvo porque o registro existente foi bloqueado.|  
|**adRecConcurrencyViolation**|0x800|Indica que o registro não foi salvo porque a simultaneidade otimista estava em uso.|  
|**adRecDBDeleted**|0x40000|Indica que o registro já foi excluído da fonte de dados.|  
|**adRecDeleted**|0x4|Indica que o registro foi excluído.|  
|**adRecIntegrityViolation**|0x1000|Indica que o registro não foi salvo porque o usuário violou as restrições de integridade.|  
|**adRecInvalid**|0x10|Indica que o registro não foi salvo porque seu indicador é inválido.|  
|**adRecMaxChangesExceeded**|0x2000|Indica que o registro não foi salvo porque havia muitas alterações pendentes.|  
|**adRecModified**|0x2|Indica que o registro foi modificado.|  
|**adRecMultipleChanges**|0x40|Indica que o registro não foi salvo porque teria afetado vários registros.|  
|**adRecNew**|0x1|Indica que o registro é novo.|  
|**adRecObjectOpen**|0x4000|Indica que o registro não foi salvo devido a um conflito com um objeto de armazenamento aberto.|  
|**adRecOK**|0|Indica que o registro foi atualizado com êxito.|  
|**adRecOutOfMemory**|0x8000|Indica que o registro não foi salvo porque o computador ficou sem memória.|  
|**adRecPendingChanges**|0x80|Indica que o registro não foi salvo porque se refere a uma inserção pendente.|  
|**adRecPermissionDenied**|0x10000|Indica que o registro não foi salvo porque o usuário não tem permissões suficientes.|  
|**adRecSchemaViolation**|0x20000|Indica que o registro não foi salvo porque viola a estrutura do banco de dados subjacente.|  
|**adRecUnmodified**|0x8|Indica que o registro não foi modificado.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 AdoEnums.RecordStatus.  
  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade Status (Conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
