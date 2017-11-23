---
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ObjectStateEnum
helpviewer_keywords: ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa1236357042126f60b27f4c6f943ae3c2198bb0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="objectstateenum"></a>ObjectStateEnum
Especifica se um objeto é aberto ou fechado, conectando a uma fonte de dados, executar um comando ou recuperar dados.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Indica que o objeto está fechado.|  
|**adStateOpen**|1|Indica que o objeto está aberto.|  
|**adStateConnecting**|2|Indica que o objeto está se conectando.|  
|**adStateExecuting**|4|Indica que o objeto é executar um comando.|  
|**adStateFetching**|8|Indica que as linhas do objeto estão sendo recuperadas.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Propriedade State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[Propriedade State (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
