---
title: CursorOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51b30e8f2ccba9dd33979f0fb3cb9cb3b6d270c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
Especifica qual funcionalidade o [suporta](../../../ado/reference/ado-api/supports-method.md) deve testar o método para.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|Oferece suporte a [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método para adicionar novos registros.|  
|**adApproxPosition**|0x4000|Oferece suporte a [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propriedades.|  
|**adBookmark**|0x2000|Oferece suporte a [indicador](../../../ado/reference/ado-api/bookmark-property-ado.md) propriedade para obter acesso a registros específicos.|  
|**adDelete**|0x1000800|Oferece suporte a [excluir](../../../ado/reference/ado-api/delete-method-ado-recordset.md) método para excluir registros.|  
|**adFind**|0x80000|Oferece suporte a [localizar](../../../ado/reference/ado-api/find-method-ado.md) método para localizar uma linha em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
|**adHoldRecords**|0x100|Recupera mais registros ou altera a próxima posição sem confirmar todas as alterações pendentes.|  
|**adIndex**|0x100000|Oferece suporte a [índice](../../../ado/reference/ado-api/index-property.md) propriedade para nomear um índice.|  
|**adMovePrevious**|0x200|Oferece suporte a [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) e [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) métodos, e [mover](../../../ado/reference/ado-api/move-method-ado.md) ou [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) métodos para mover o registro atual posição para trás sem a necessidade de indicadores.|  
|**adNotify**|0x40000|Indica que o provedor de dados subjacente oferece suporte a notificações (que determina se **registros** eventos são suportados).|  
|**adResync**|0x20000|Oferece suporte a [Resync](../../../ado/reference/ado-api/resync-method.md) método para atualizar o cursor com os dados que está visíveis no banco de dados subjacente.|  
|**adSeek**|0x200000|Oferece suporte a [busca](../../../ado/reference/ado-api/seek-method.md) método para localizar uma linha em uma **registros**.|  
|**adUpdate**|0x1008000|Oferece suporte a [atualização](../../../ado/reference/ado-api/update-method.md) método para modificar os dados existentes.|  
|**adUpdateBatch**|0x10000|Oferece suporte a atualização em lotes ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) e [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos) para transmitir grupos de alterações no provedor.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorOption.ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums.CursorOption.BOOKMARK|  
|AdoEnums.CursorOption.DELETE|  
|AdoEnums.CursorOption.FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums.CursorOption.INDEX|  
|AdoEnums.CursorOption.MOVEPREVIOUS|  
|AdoEnums.CursorOption.NOTIFY|  
|AdoEnums.CursorOption.RESYNC|  
|AdoEnums.CursorOption.SEEK|  
|AdoEnums.CursorOption.UPDATE|  
|AdoEnums.CursorOption.UPDATEBATCH|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
