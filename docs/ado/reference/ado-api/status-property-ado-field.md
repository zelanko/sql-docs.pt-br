---
title: A propriedade de status (campo ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d8554902e965fc58ea4bc83a97512944ed146a9e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="status-property-ado-field"></a>Propriedade de status (campo ADO)
Indica o status de um [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) valor. O valor padrão é **adFieldOK**.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="record-field-status"></a>Status de campo do registro  
 Altera para o valor de um **campo** objeto na coleção de campos de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto são armazenados em cache até que o objeto [atualização](../../../ado/reference/ado-api/update-method.md) método é chamado. Nesse ponto, se a alteração para o valor do campo causou um erro, o OLE DB gera o erro **DB_E_ERRORSOCCURRED** (2147749409). A propriedade de Status de qualquer um do **campo** objetos no **campos** coleção que causou o erro conterá um valor da [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) que descreve a causa do o problema.  
  
 Para melhorar o desempenho, adições e exclusões para o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleções do **registro** objeto são armazenados em cache até que o **atualização** método é chamado e, em seguida, as alterações são feitas em uma atualização otimista em lotes. Se o **atualização** método não for chamado, o servidor não está atualizado. Se todas as atualizações falharem, será retornado um erro de provedor do OLE DB (DB_E_ERRORSOCCURRED) e o **Status** propriedade indica valores combinados do código de status de operação e o erro. Por exemplo, **adFieldPendingInsert adFieldPermissionDenied ou**. O **Status** propriedade para cada **campo** pode ser usado para determinar por que o **campo** foi adicionada, modificada ou excluída não.  
  
 Muitos tipos de problemas encontrados ao adicionar, modificar ou excluir um **campo** são relatados por meio de **Status** propriedade. Por exemplo, se o usuário exclui uma **campo**, ela está marcada para exclusão a **campos** coleção. Se o subsequentes **atualização** retorna um erro porque o usuário tentou excluir uma **campo** para os quais não têm permissão, o **campo** terá um  **Status** de **adFieldPermissionDenied adFieldPendingDelete ou**. Chamando o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) valores originais de restaurações de método e define o **Status** para **adFieldOK**.  
  
 Da mesma forma, o **atualização** método pode retornar um erro porque um novo **campo** foi adicionada e recebe um valor inadequado. Nesse caso, o novo **campo** no **campos** coleta e ter um status de **adFieldPendingInsert** e talvez **adFieldCantCreate** (dependendo de seu provedor). Você pode fornecer um valor apropriado para o novo **campo** e chame **atualização** novamente.  
  
## <a name="recordset-field-status"></a>Status de campo do conjunto de registros  
 Altera para o valor de um **campo** objeto da coleção de campos de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) são armazenados em cache até que o objeto [atualização](../../../ado/reference/ado-api/update-method.md) método é chamado. Nesse ponto, se a alteração para o valor do campo causou um erro, o OLE DB gera o erro **DB_E_ERRORSOCCURRED** (2147749409). A propriedade de Status de qualquer um do **campo** objetos no **campos** coleção que causou o erro conterá um valor da [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) que descreve a causa do o problema.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade status (campo) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Exemplo da propriedade Status (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
