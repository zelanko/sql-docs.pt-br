---
title: ObjectStateEnum | Microsoft Docs
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
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf7bdb66b8c8de0e45417e85005d7eda90fdc014
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="objectstateenum"></a>ObjectStateEnum
Especifica se um objeto é aberto ou fechado, conectando a uma fonte de dados, executar um comando ou recuperar dados.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Indica que o objeto está fechado.|  
|**adStateOpen**|1|Indica que o objeto está aberto.|  
|**adStateConnecting**|2|Indica que o objeto está se conectando.|  
|**adStateExecuting**|4|Indica que o objeto é executar um comando.|  
|**adStateFetching**|8|Indica que as linhas do objeto estão sendo recuperadas.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC Equivalent  
 Package: **com.ms.wfc.data**  
  
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
