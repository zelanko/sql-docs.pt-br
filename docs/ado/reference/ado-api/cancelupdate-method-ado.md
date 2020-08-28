---
description: Método CancelUpdate (ADO)
title: Método CancelUpdate (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
author: rothja
ms.author: jroth
ms.openlocfilehash: 2355d2a0b2ff0bbe14eb9b7d2a9a373164a4f5e5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975557"
---
# <a name="cancelupdate-method-ado"></a>Método CancelUpdate (ADO)
Cancela as alterações feitas na linha atual ou nova de um objeto [Recordset](./recordset-object-ado.md) ou na coleção [Fields](./fields-collection-ado.md) de um objeto [Record](./record-object-ado.md) , antes de chamar o método [Update](./update-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>Comentários  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o método **CancelUpdate** para cancelar as alterações feitas na linha atual ou para descartar uma linha recém-adicionada. Não é possível cancelar as alterações na linha atual ou em uma nova linha depois de chamar o método **Update** , a menos que as alterações façam parte de uma transação que você possa reverter com o método [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) ou parte de uma atualização do lote. No caso de uma atualização em lotes, você pode cancelar a **atualização** com o método **CancelUpdate** ou [CancelBatch](./cancelbatch-method-ado.md) .  
  
 Se você estiver adicionando uma nova linha ao chamar o método **CancelUpdate** , a linha atual se tornará a linha que era atual antes da chamada [AddNew](./addnew-method-ado.md) .  
  
 Se você estiver no modo de edição e quiser sair do registro atual (por exemplo, usando os métodos [move](./move-method-ado.md), [NextRecordset](./nextrecordset-method-ado.md)ou [Close](./close-method-ado.md) ), poderá usar o **CancelUpdate** para cancelar as alterações pendentes. Talvez seja necessário fazer isso se a atualização não puder ser postada com êxito à fonte de dados. Por exemplo, uma tentativa de exclusão que falha devido a violações de integridade referencial deixará o **conjunto de registros** no modo de edição após uma chamada para [delete](./delete-method-ado-recordset.md).  
  
## <a name="record"></a>Record  
 O método **CancelUpdate** cancela todas as inserções ou exclusões pendentes de objetos de [campo](./field-object.md) e cancela atualizações pendentes de campos existentes e os restaura aos valores originais. A propriedade [status](./status-property-ado-recordset.md) de todos os campos na coleção **Fields** é definida como **adFieldOK**.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Coleção Fields (ADO)](./fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Recordset (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Update e CancelUpdate (VB)](./update-and-cancelupdate-methods-example-vb.md)   
 [Exemplo dos métodos Update e CancelUpdate (VC + +)](./update-and-cancelupdate-methods-example-vc.md)   
 [Método AddNew (ADO)](./addnew-method-ado.md)   
 [Método Cancel (ADO)](./cancel-method-ado.md)   
 [Método Cancel (RDS)](../rds-api/cancel-method-rds.md)   
 [Método CancelBatch (ADO)](./cancelbatch-method-ado.md)   
 [Método CancelUpdate (RDS)](../rds-api/cancelupdate-method-rds.md)   
 [Propriedade EditMode](./editmode-property.md)   
 [Método Update](./update-method.md)