---
description: IsolationLevelEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 03bd95a642f3942275e1ff9d32f1b2d1829b96d3
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774685"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
Especifica o nível de isolamento de transação para um objeto de [conexão](./connection-object-ado.md) .  
  
|Constante|Valor|Descrição|  
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
 [Propriedade IsolationLevel](./isolationlevel-property.md)