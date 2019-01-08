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
manager: craigg
ms.openlocfilehash: 89cab313736a8d5acf2f7796ea79fb5649f85ab2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52525870"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
Especifica o grupo de registros a serem filtrados de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|Filtros para exibir apenas os registros afetados pela última [exclua](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [ressincronizar](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) chamar.|  
|**adFilterConflictingRecords**|5|Filtros para exibir os registros que falharam na última atualização em lotes.|  
|**adFilterFetchedRecords**|3|Filtros para exibir os registros no cache atual – ou seja, os resultados da última chamada para recuperar os registros do banco de dados.|  
|**adFilterNone**|0|Remove o filtro atual e restaura todos os registros para exibição.|  
|**adFilterPendingRecords**|1|Filtros para exibir apenas os registros que foram alterados, mas ainda não foram enviados ao servidor. Aplicável somente para o modo de atualização em lotes.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
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
