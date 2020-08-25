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
ms.openlocfilehash: 83ba6960e6e7f81db55f3a8292fd054c1377b106
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775515"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
Especifica a funcionalidade para a qual o método de [suporte](./supports-method.md) deve ser testado.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|Dá suporte ao método [AddNew](./addnew-method-ado.md) para adicionar novos registros.|  
|**adApproxPosition**|0x4000|Dá suporte às propriedades [AbsolutePosition](./absoluteposition-property-ado.md) e [AbsolutePage](./absolutepage-property-ado.md) .|  
|**adBookmark**|0x2000|Dá suporte à propriedade [Bookmark](./bookmark-property-ado.md) para obter acesso a registros específicos.|  
|**adDelete**|0x1000800|Dá suporte ao método [delete](./delete-method-ado-recordset.md) para excluir registros.|  
|**Find**|0x80000|Dá suporte ao método [Find](./find-method-ado.md) para localizar uma linha em um [conjunto de registros](./recordset-object-ado.md).|  
|**adHoldRecords**|0x100|Recupera mais registros ou altera a próxima posição sem confirmar todas as alterações pendentes.|  
|**adIndex**|0x100000|Dá suporte à propriedade [index](./index-property.md) para nomear um índice.|  
|**adMovePrevious**|0x200|Dá suporte aos métodos [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) e [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) , e os métodos [move](./move-method-ado.md) ou [GetRows](./getrows-method-ado.md) para mover a posição do registro atual para trás sem a necessidade de indicadores.|  
|**adNotify**|0x40000|Indica que o provedor de dados subjacente oferece suporte a notificações (que determina se há suporte para os eventos do **conjunto de registros** ).|  
|**adResync**|0x20000|Dá suporte ao método [Ressync](./resync-method.md) para atualizar o cursor com os dados que estão visíveis no banco de dado subjacente.|  
|**adSeek**|0x200000|Dá suporte ao método [Seek](./seek-method.md) para localizar uma linha em um **conjunto de registros**.|  
|**adUpdate**|0x1008000|Dá suporte ao método [Update](./update-method.md) para modificar os dados existentes.|  
|**adUpdateBatch**|0x10000|Dá suporte à atualização em lotes (métodos[UpdateBatch](./updatebatch-method.md) e [CancelBatch](./cancelbatch-method-ado.md) ) para transmitir grupos de alterações para o provedor.|  
  
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
 [Método Supports](./supports-method.md)