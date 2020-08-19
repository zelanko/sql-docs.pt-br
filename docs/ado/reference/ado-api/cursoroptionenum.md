---
description: CursorOptionEnum
title: CursorOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
author: rothja
ms.author: jroth
ms.openlocfilehash: 35846bf873ff98ff15e2581c36e1963b7ddcd08c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444268"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
Especifica a funcionalidade para a qual o método de [suporte](../../../ado/reference/ado-api/supports-method.md) deve ser testado.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|Dá suporte ao método [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) para adicionar novos registros.|  
|**adApproxPosition**|0x4000|Dá suporte às propriedades [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) .|  
|**adBookmark**|0x2000|Dá suporte à propriedade [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md) para obter acesso a registros específicos.|  
|**adDelete**|0x1000800|Dá suporte ao método [delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) para excluir registros.|  
|**Find**|0x80000|Dá suporte ao método [Find](../../../ado/reference/ado-api/find-method-ado.md) para localizar uma linha em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adHoldRecords**|0x100|Recupera mais registros ou altera a próxima posição sem confirmar todas as alterações pendentes.|  
|**adIndex**|0x100000|Dá suporte à propriedade [index](../../../ado/reference/ado-api/index-property.md) para nomear um índice.|  
|**adMovePrevious**|0x200|Dá suporte aos métodos [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) e [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) , e os métodos [move](../../../ado/reference/ado-api/move-method-ado.md) ou [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) para mover a posição do registro atual para trás sem a necessidade de indicadores.|  
|**adNotify**|0x40000|Indica que o provedor de dados subjacente oferece suporte a notificações (que determina se há suporte para os eventos do **conjunto de registros** ).|  
|**adResync**|0x20000|Dá suporte ao método [Ressync](../../../ado/reference/ado-api/resync-method.md) para atualizar o cursor com os dados que estão visíveis no banco de dado subjacente.|  
|**adSeek**|0x200000|Dá suporte ao método [Seek](../../../ado/reference/ado-api/seek-method.md) para localizar uma linha em um **conjunto de registros**.|  
|**adUpdate**|0x1008000|Dá suporte ao método [Update](../../../ado/reference/ado-api/update-method.md) para modificar os dados existentes.|  
|**adUpdateBatch**|0x10000|Dá suporte à atualização em lotes (métodos[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) e [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) ) para transmitir grupos de alterações para o provedor.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. CursorOption. ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums. CursorOption. BOOKMARK|  
|AdoEnums. CursorOption. DELETE|  
|AdoEnums. CursorOption. FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums. CursorOption. INDEX|  
|AdoEnums. CursorOption. MOVEPREVIOUS|  
|AdoEnums. CursorOption. NOTIFY|  
|AdoEnums. CursorOption. ressincronização|  
|AdoEnums. CursorOption. SEEK|  
|AdoEnums. CursorOption. UPDATE|  
|AdoEnums. CursorOption. UPDATEBATCH|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
