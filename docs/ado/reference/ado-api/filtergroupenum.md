---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97add08a1d656e8c163600bb0ea8dda7fca264b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932641"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
Especifica o grupo de registros a ser filtrado de um [conjunto](../../../ado/reference/ado-api/recordset-object-ado.md)de registros.  
  
|Constante|Valor|DESCRIÇÃO|  
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
