---
title: Propriedade CursorType (ADO) | Microsoft Docs
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
f1_keywords: Recordset15::CursorType
helpviewer_keywords: CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f1f16755e5030cec19d7b513f725f3fd5defb3f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="cursortype-property-ado"></a>Propriedade CursorType (ADO)
Indica o tipo de cursor usado em uma [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valor. O valor padrão é **adOpenForwardOnly**.  
  
## <a name="remarks"></a>Comentários  
 Use o **CursorType** propriedade para especificar o tipo de cursor que deve ser usada ao abrir o **registros** objeto.  
  
 Somente uma configuração de **adOpenStatic** terá suporte se o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está definida como **adUseClient**. Se for definido um valor sem suporte, nenhum erro ocorrerá; suporte a mais próximo **CursorType** será usado.  
  
 Se um provedor não oferece suporte para o tipo de cursor solicitado, ele pode retornar a outro tipo de cursor. O **CursorType** propriedade será alterada para corresponder ao tipo de cursor real em uso quando o [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto está aberto. Para verificar a funcionalidade específica do cursor retornado, use o [suporta](../../../ado/reference/ado-api/supports-method.md) método. Depois de fechar o **registros**, o **CursorType** propriedade é revertida para sua configuração original.  
  
 O gráfico a seguir mostra a funcionalidade de provedor (identificado por **suporta** constantes do método) necessária para cada tipo de cursor.  
  
|Para um conjunto de registros desse CursorType|O método dá suporte à deve retornar True para todas as constantes|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  Embora **dá suporte a**(**adUpdateBatch**) pode ser verdadeiro para cursores dinâmicos e de somente avanço, para atualizações de lote, você deve usar um conjunto de chaves ou um cursor estático. Definir o [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) propriedade **adLockBatchOptimistic** e o **CursorLocation** propriedade **adUseClient** para habilitar o Cursor Serviço do OLE DB, que é necessário para as atualizações em lotes.  
  
 O **CursorType** propriedade é leitura/gravação quando o **registros** é fechado e somente leitura quando ela é aberta.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **registros** objeto, o **CursorType** propriedade pode ser definida somente como **adOpenStatic**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades EditMode (VB), CursorType e LockType](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Exemplo de propriedades EditMode (VC + +), CursorType e LockType](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
