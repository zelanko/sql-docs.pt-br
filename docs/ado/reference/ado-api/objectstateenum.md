---
title: ObjectStateEnum | Microsoft Docs
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
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be8153e48ce652acd713633114e6a21d4a22721a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

