---
title: IsolationLevelEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15ae2aac2851c496b6cac9e47d37fe5fa26b8e34
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918371"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
Especifica o nível de isolamento de transação para um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
|Constante|Valor|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|Indica que o provedor está usando um nível de isolamento diferente do especificado, mas que o nível não pode ser determinado.|  
|**adXactChaos**|16|Indica que as alterações pendentes de transações mais isoladas não podem ser substituídas.|  
|**adXactBrowse**|256|Indica que, em uma transação, você pode exibir alterações não confirmadas em outras transações.|  
|**adXactReadUncommitted**|256|O mesmo que **adXactBrowse**.|  
|**adXactCursorStability**|4096|Indica que, em uma transação, você pode exibir alterações em outras transações somente depois que elas tiverem sido confirmadas.|  
|**adXactReadCommitted**|4096|O mesmo que **adXactCursorStability**.|  
|**adXactRepeatableRead**|65536|Indica que, em uma transação, você não pode ver as alterações feitas em outras transações, mas essa reconsulta pode recuperar novos objetos de **conjunto de registros** .|  
|**adXactIsolated**|1048576|Indica que as transações são conduzidas no isolamento de outras transações.|  
|**adXactSerializable**|1048576|O mesmo que **adXactIsolated**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. IsolationLevel. não especificado|  
|AdoEnums. IsolationLevel. caos|  
|AdoEnums. IsolationLevel. BROWSE|  
|AdoEnums. IsolationLevel. READUNCOMMITTED|  
|AdoEnums. IsolationLevel. CURSORSTABILITY|  
|AdoEnums. IsolationLevel. READCOMMITTED|  
|AdoEnums. IsolationLevel. REPEATABLEREAD|  
|AdoEnums. IsolationLevel. ISOLAted|  
|AdoEnums. IsolationLevel. SERIALIZABLE|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)
