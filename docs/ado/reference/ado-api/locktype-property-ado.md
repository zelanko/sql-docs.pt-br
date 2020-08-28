---
description: Propriedade LockType (ADO)
title: Propriedade LockType (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
author: rothja
ms.author: jroth
ms.openlocfilehash: 74e86b054ac9d63527cc0f142ee50aa81acbe4b4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990687"
---
# <a name="locktype-property-ado"></a>Propriedade LockType (ADO)
Indica o tipo de bloqueios colocados em registros durante a edição.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [LockTypeEnum](./locktypeenum.md) . O valor padrão é **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentários  
 Defina a propriedade **LockType** antes de abrir um [conjunto de registros](./recordset-object-ado.md) para especificar o tipo de bloqueio que o provedor deve usar ao abri-lo. Leia a propriedade para retornar o tipo de bloqueio em uso em um objeto Open **Recordset** .  
  
 Os provedores podem não dar suporte a todos os tipos de bloqueio. Se um provedor não puder oferecer suporte à configuração **LockType** solicitada, ele substituirá outro tipo de bloqueio. Para determinar a funcionalidade de bloqueio real disponível em um objeto **Recordset** , use o método com [suporte](./supports-method.md) com **adUpdate** e **adUpdateBatch**.  
  
 A configuração **adLockPessimistic** não terá suporte se a propriedade [CursorLocation](./cursorlocation-property-ado.md) estiver definida como **adUseClient**. Se um valor sem suporte for definido, nenhum erro será resultado; o **LockType** com suporte mais próximo será usado em seu lugar.  
  
 A propriedade **LockType** é leitura/gravação quando o **conjunto de registros** é fechado e somente leitura quando é aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um objeto **Recordset** do lado do cliente, a propriedade **LockType** só pode ser definida como **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades CursorType, LockType e EditMode (VB)](./cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Exemplo das propriedades CursorType, LockType e EditMode (VC + +)](./cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método CancelBatch (ADO)](./cancelbatch-method-ado.md)   
 [Método UpdateBatch](./updatebatch-method.md)