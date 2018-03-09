---
title: LockTypeEnum | Microsoft Docs
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
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f9fe62c251092eb182925de0fa7b6d70c359a25d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="locktypeenum"></a>LockTypeEnum
Especifica o tipo de bloqueio colocado em registros durante a edição.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|Indica as atualizações em lotes otimista. Necessário para o modo de atualização em lotes.|  
|**adLockOptimistic**|3|Indica o bloqueio otimista, registro por registro. O provedor usa bloqueio otimista, bloqueando registros somente quando você chamar o [atualização](../../../ado/reference/ado-api/update-method.md) método.|  
|**adLockPessimistic**|2|Indica o bloqueio pessimista, registro por registro. O provedor não o que é necessário para garantir êxito edição dos registros, normalmente por bloqueando registros na fonte de dados imediatamente após a edição.|  
|**adLockReadOnly**|1|Indica os registros de somente leitura. Você não pode alterar os dados.|  
|**adLockUnspecified**|-1|Não especifique um tipo de bloqueio. Para clones, o clone é criado com o mesmo tipo de bloqueio que o original.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC Equivalent  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums.LockType.OPTIMISTIC|  
|AdoEnums.LockType.PESSIMISTIC|  
|AdoEnums.LockType.READONLY|  
|AdoEnums.LockType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método Clone (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[Propriedade LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Método Open (Conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
