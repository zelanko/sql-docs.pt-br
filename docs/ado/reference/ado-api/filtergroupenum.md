---
title: FilterGroupEnum | Microsoft Docs
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
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 424bb4b32915c774778cfd32dab18c42c5e573a8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="filtergroupenum"></a>FilterGroupEnum
Especifica o grupo de registros a ser filtrada de uma [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|Filtros para exibir apenas os registros afetados pela última [excluir](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) chamar.|  
|**adFilterConflictingRecords**|5|Filtros para exibir os registros que falharam na última atualização em lotes.|  
|**adFilterFetchedRecords**|3|Filtros para exibir os registros no cache atual — ou seja, os resultados da última chamada para recuperar os registros do banco de dados.|  
|**adFilterNone**|0|Remove o filtro atual e restaura todos os registros para exibição.|  
|**adFilterPendingRecords**|1|Os filtros para exibir somente os registros que foram alterados mas ainda não foram enviados ao servidor. Aplicável somente para o modo de atualização em lotes.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums.FilterGroup.NONE|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade Filter](../../../ado/reference/ado-api/filter-property.md)

