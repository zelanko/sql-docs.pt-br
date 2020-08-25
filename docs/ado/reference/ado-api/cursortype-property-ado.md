---
description: Propriedade CursorType (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a85bb0f624c5f5a3100bfba5d33d63a574fa9d0e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775495"
---
# <a name="cursortype-property-ado"></a>Propriedade CursorType (ADO)
Indica o tipo de cursor usado em um objeto [Recordset](./recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [CursorTypeEnum](./cursortypeenum.md) . O valor padrão é **adOpenForwardOnly**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **CursorType** para especificar o tipo de cursor que deve ser usado ao abrir o objeto **Recordset** .  
  
 Somente uma configuração de **adOpenStatic** terá suporte se a propriedade [CursorLocation](./cursorlocation-property-ado.md) estiver definida como **adUseClient**. Se um valor sem suporte for definido, nenhum erro será resultado; o **CursorType** com suporte mais próximo será usado em seu lugar.  
  
 Se um provedor não oferecer suporte ao tipo de cursor solicitado, ele poderá retornar outro tipo de cursor. A propriedade **CursorType** será alterada para corresponder ao tipo de cursor real em uso quando o objeto [Recordset](./recordset-object-ado.md) estiver aberto. Para verificar a funcionalidade específica do cursor retornado, use o método [com suporte](./supports-method.md) . Depois de fechar o **conjunto de registros**, a propriedade **CursorType** reverte para sua configuração original.  
  
 O gráfico a seguir mostra a funcionalidade do provedor (identificada por **suporte** a constantes do método) necessária para cada tipo de cursor.  
  
|Para um conjunto de registros deste CursorType|O método de suporte deve retornar true para todas essas constantes|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|nenhum|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  Embora **suporte**(**adUpdateBatch**) possa ser verdadeiro para cursores dinâmicos e somente de avanço, para atualizações em lotes, você deve usar um conjunto de chaves ou um cursor estático. Defina a propriedade [LockType](./locktype-property-ado.md) como **adLockBatchOptimistic** e a propriedade **CursorLocation** como **adUseClient** para habilitar o serviço de cursor para OLE DB, que é necessário para atualizações em lote.  
  
 A propriedade **CursorType** é de leitura/gravação quando o **conjunto de registros** é fechado e somente leitura quando é aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um objeto **Recordset** do lado do cliente, a propriedade **CursorType** pode ser definida somente como **adOpenStatic**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades CursorType, LockType e EditMode (VB)](./cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Exemplo das propriedades CursorType, LockType e EditMode (VC + +)](./cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método Supports](./supports-method.md)