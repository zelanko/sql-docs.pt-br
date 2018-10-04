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
manager: craigg
ms.openlocfilehash: 366892f51207e7d89f643510f9becb664bb098c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684194"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
Especifica o nível de isolamento da transação para um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|Indica que o provedor está usando um nível de isolamento diferente do que o especificado, mas que não é possível determinar o nível.|  
|**adXactChaos**|16|Indica que alterações pendentes de transações maior isolamento não pode ser substituído.|  
|**adXactBrowse**|256|Indica que, de uma transação seja possível visualizar as alterações não confirmadas em outras transações.|  
|**adXactReadUncommitted**|256|Mesmo que **adXactBrowse**.|  
|**adXactCursorStability**|4096|Indica que em uma transação você pode exibir as alterações em outras transações somente depois de terem sido confirmados.|  
|**adXactReadCommitted**|4096|Mesmo que **adXactCursorStability**.|  
|**adXactRepeatableRead**|65536|Indica que a partir de uma transação, você não pode ver as alterações feitas em outras transações, mas que repetir a consulta pode recuperar novos **Recordset** objetos.|  
|**adXactIsolated**|1048576|Indica que as transações sejam realizadas em isolamento de outras transações.|  
|**adXactSerializable**|1048576|Mesmo que **adXactIsolated**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.IsolationLevel.UNSPECIFIED|  
|AdoEnums.IsolationLevel.CHAOS|  
|AdoEnums.IsolationLevel.BROWSE|  
|AdoEnums.IsolationLevel.READUNCOMMITTED|  
|AdoEnums.IsolationLevel.CURSORSTABILITY|  
|AdoEnums.IsolationLevel.READCOMMITTED|  
|AdoEnums.IsolationLevel.REPEATABLEREAD|  
|AdoEnums.IsolationLevel.ISOLATED|  
|AdoEnums.IsolationLevel.SERIALIZABLE|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)
