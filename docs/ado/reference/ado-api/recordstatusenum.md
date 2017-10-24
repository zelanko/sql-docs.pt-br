---
title: RecordStatusEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bf2413bed1bbdf96b83b7e805aac90529a721c9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="recordstatusenum"></a>RecordStatusEnum
Especifica o [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) de um registro em relação a atualizações em lotes e outras operações em massa.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|Indica que o registro não foi salva porque a operação foi cancelada.|  
|**adRecCantRelease**|0x400|Indica que o novo registro não foi salva porque o registro existente foi bloqueado.|  
|**adRecConcurrencyViolation**|0x800|Indica que o registro não foi salva porque a simultaneidade otimista estava em uso.|  
|**adRecDBDeleted**|0x40000|Indica que o registro foi excluído da fonte de dados.|  
|**adRecDeleted**|0x4|Indica que o registro foi excluído.|  
|**adRecIntegrityViolation**|0x1000|Indica que o registro não foi salva porque o usuário violou as restrições de integridade.|  
|**adRecInvalid**|0x10|Indica que o registro não foi salva porque seu indicador é inválido.|  
|**adRecMaxChangesExceeded**|0x2000|Indica que o registro não foi salva porque havia muitos alterações pendentes.|  
|**adRecModified**|0x2|Indica que o registro foi modificado.|  
|**adRecMultipleChanges**|0x40|Indica que o registro não foi salva porque ela teria afetado vários registros.|  
|**adRecNew**|0x1|Indica que o registro é novo.|  
|**adRecObjectOpen**|0x4000|Indica que o registro não foi salvo devido a um conflito com um objeto de armazenamento aberto.|  
|**adRecOK**|0|Indica que o registro foi atualizado com êxito.|  
|**adRecOutOfMemory**|0x8000|Indica que o registro não foi salva porque o computador ficou sem memória.|  
|**adRecPendingChanges**|0x80|Indica que o registro não foi salva porque ela se refere a uma inserção pendente.|  
|**adRecPermissionDenied**|0x10000|Indica que o registro não foi salva porque o usuário não tem permissões suficientes.|  
|**adRecSchemaViolation**|0x20000|Indica que o registro não foi salva porque ela viola a estrutura do banco de dados subjacente.|  
|**adRecUnmodified**|0x8|Indica que o registro não foi modificado.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 AdoEnums.RecordStatus.  
  
 Pacote: **com.ms.wfc.data**  
  
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
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade Status (Conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md)

