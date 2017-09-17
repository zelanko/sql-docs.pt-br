---
title: Propriedade LockType (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b2f293565affedf74facb22fffc85b3b2ead179
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="locktype-property-ado"></a>Propriedade LockType (ADO)
Indica o tipo de bloqueios colocados em registros durante a edição.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor. O valor padrão é **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentários  
 Definir o **LockType** propriedade antes de abrir um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) para especificar o tipo de bloqueio do provedor deve usar ao abri-lo. Ler a propriedade para retornar o tipo de bloqueio em uso em um aberto **registros** objeto.  
  
 Provedores podem não suportar todos os tipos de bloqueio. Se um provedor não oferecer suporte a solicitação **LockType** configuração, ele substituirá outro tipo de bloqueio. Para determinar a funcionalidade de bloqueio real em um **registros** de objeto, use o [dá suporte a](../../../ado/reference/ado-api/supports-method.md) método com **adUpdate** e **adUpdateBatch**.  
  
 O **adLockPessimistic** configuração não é suportada se o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está definida como **adUseClient**. Se for definido um valor sem suporte, nenhum erro ocorrerá; suporte a mais próximo **LockType** será usado.  
  
 O **LockType** propriedade é leitura/gravação quando o **registros** é fechado e somente leitura quando ela é aberta.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **registros** objeto, o **LockType** propriedade só pode ser definida como **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades EditMode (VB), CursorType e LockType](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Exemplo de propriedades EditMode (VC + +), CursorType e LockType](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

