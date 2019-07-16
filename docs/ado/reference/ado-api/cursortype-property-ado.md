---
title: Propriedade CursorType (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4dc881b96a1e2641d4946340c9462455197f2043
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919251"
---
# <a name="cursortype-property-ado"></a>Propriedade CursorType (ADO)
Indica o tipo de cursor usado em uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valor. O valor padrão é **adOpenForwardOnly**.  
  
## <a name="remarks"></a>Comentários  
 Use o **CursorType** propriedade para especificar o tipo de cursor que deve ser usado ao abrir o **Recordset** objeto.  
  
 Somente uma configuração de **adOpenStatic** terá suporte se o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) estiver definida como **adUseClient**. Se um valor sem suporte for definido, nenhum erro ocorrerá; suporte a mais próxima **CursorType** será usado.  
  
 Se um provedor não oferece suporte para o tipo de cursor solicitado, ele poderá retornar outro tipo de cursor. O **CursorType** propriedade será alterada para corresponder ao tipo de cursor real em uso quando o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto está aberto. Para verificar a funcionalidade específica do cursor retornado, use o [dá suporte a](../../../ado/reference/ado-api/supports-method.md) método. Depois de fechar o **conjunto de registros**, o **CursorType** propriedade será revertida para sua configuração original.  
  
 O gráfico a seguir mostra a funcionalidade de provedor (identificado por **dá suporte a** constantes do método) necessárias para cada tipo de cursor.  
  
|Para um conjunto de registros desse CursorType|O método dá suporte a deve retornar True para todas as constantes|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|nenhum|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  Embora **suporta**(**adUpdateBatch**) pode ser verdadeiro para cursores dinâmicos e de somente avanço, para atualizações de lote, você deve usar um conjunto de chaves ou um cursor estático. Definir a [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) propriedade a ser **adLockBatchOptimistic** e o **CursorLocation** propriedade **adUseClient** para habilitar o Cursor Serviço do OLE DB, que é necessário para atualizações em lotes.  
  
 O **CursorType** propriedade é leitura/gravação quando o **Recordset** é fechada e somente leitura quando ele é aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **conjunto de registros** objeto, o **CursorType** propriedade pode ser definida somente como **adOpenStatic**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [CursorType, LockType, EditMode exemplo das propriedades e (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType, EditMode exemplo das propriedades e (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
