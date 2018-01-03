---
title: "Atualizar a ressincronização de propriedade dinâmica (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64f0b19708dcb2a2333e800ba9cddb5b092ba04a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="update-resync-property-dynamic-ado"></a>Atualização ressincronização propriedade dinâmica (ADO)
Especifica se o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método é seguido por um implícita [Resync](../../../ado/reference/ado-api/resync-method.md) operação de método e nesse caso, o escopo dessa operação.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna uma ou mais do [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) valores.  
  
## <a name="remarks"></a>Remarks  
 Os valores de ADCPROP_UPDATERESYNC_ENUM podem ser combinados, exceto adResyncAll que já representa a combinação do restante dos valores.  
  
 A constante **adResyncConflicts** armazena os valores de ressincronização como valores subjacentes, mas não substitui as alterações pendentes.  
  
 **Atualizar ressincronização** é uma propriedade dinâmica anexada ao [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
