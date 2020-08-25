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
ms.openlocfilehash: 7552eb4b069b2cd2adc33e0bff25f23d918468c2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775285"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
Especifica o grupo de registros a ser filtrado de um [conjunto](./recordset-object-ado.md)de registros.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|Filtros para exibir somente os registros afetados pela última chamada de [exclusão](./delete-method-ado-recordset.md), [ressincronização](./resync-method.md), [UpdateBatch](./updatebatch-method.md)ou [CancelBatch](./cancelbatch-method-ado.md) .|  
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
 [Propriedade Filter](./filter-property.md)