---
title: Propriedade LockType (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05670439a8f14018a999557dd135912e0c2e0159
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736014"
---
# <a name="locktype-property-ado"></a>Propriedade LockType (ADO)
Indica o tipo de bloqueios são colocados nos registros durante a edição.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor. O valor padrão é **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentários  
 Defina as **LockType** propriedade antes de abrir um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para especificar que tipo de bloqueio do provedor deve usar ao abri-lo. Ler a propriedade para retornar o tipo de bloqueio em uso em um aberto **Recordset** objeto.  
  
 Provedores podem não dar suporte a todos os tipos de bloqueio. Se um provedor não oferecer suporte a solicitada **LockType** configuração, ele substituirá outro tipo de bloqueio. Para determinar a funcionalidade de bloqueio real em um **conjunto de registros** do objeto, use o [dá suporte à](../../../ado/reference/ado-api/supports-method.md) método com **adUpdate** e **adUpdateBatch**.  
  
 O **adLockPessimistic** configuração não tem suporte se o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) estiver definida como **adUseClient**. Se um valor sem suporte for definido, nenhum erro ocorrerá; suporte a mais próxima **LockType** será usado.  
  
 O **LockType** propriedade é leitura/gravação quando o **Recordset** é fechada e somente leitura quando ele é aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **conjunto de registros** objeto, o **LockType** propriedade só pode ser definida como **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [CursorType, LockType, EditMode exemplo das propriedades e (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType, EditMode exemplo das propriedades e (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
