---
title: Propriedade status (campo ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a647051e7953d6f2977074feda94cf7e9f3d9d82
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711018"
---
# <a name="status-property-ado-field"></a>Propriedade Status (campo ADO)
Indica o status de uma [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) valor. O valor padrão é **adFieldOK**.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="record-field-status"></a>Status de campo do registro  
 Altera para o valor de uma **campo** objeto da coleção de campos de uma [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto são armazenadas em cache até que o objeto [atualização](../../../ado/reference/ado-api/update-method.md) método é chamado. Nesse ponto, se a alteração para o valor do campo causou um erro, o OLE DB gera o erro **DB_E_ERRORSOCCURRED** (2147749409). A propriedade de Status de qualquer um dos **campo** objetos na **campos** coleção que causou o erro conterá um valor da [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) que descreve a causa da o problema.  
  
 Para melhorar o desempenho, adições e exclusões para o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleções da **registro** objeto são armazenadas em cache até que o **atualização** método é chamado e, em seguida, as alterações são feitas em uma atualização otimista de lote. Se o **atualização** método não é chamado, o servidor não será atualizado. Se todas as atualizações falharem, será retornado um erro de provedor do OLE DB (DB_E_ERRORSOCCURRED) e o **Status** propriedade indica os valores combinados do código de status de operação e erro. Por exemplo, **adFieldPendingInsert adFieldPermissionDenied OR**. O **Status** propriedade para cada **campo** pode ser usado para determinar por que o **campo** foi adicionada, modificada ou excluída não.  
  
 Muitos tipos de problemas encontrados ao adicionar, modificar ou excluir uma **campo** são relatados por meio de **Status** propriedade. Por exemplo, se o usuário exclui um **campo**, ele é marcado para exclusão da **campos** coleção. Se o subsequentes **atualização** retorna um erro porque o usuário tentou excluir um **campo** para os quais não têm permissão, o **campo** terão uma  **Status** dos **adFieldPermissionDenied adFieldPendingDelete OR**. Chamar o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) valores originais do método restaurações e define o **Status** para **adFieldOK**.  
  
 Da mesma forma, o **atualização** método pode retornar um erro porque uma nova **campo** foi adicionada e recebe um valor inadequado. Nesse caso, o novo **campo** estará na **campos** coleção e ter um status de **adFieldPendingInsert** e, talvez, **adFieldCantCreate** (dependendo de seu provedor). Você pode fornecer um valor apropriado para o novo **campo** e chame **atualização** novamente.  
  
## <a name="recordset-field-status"></a>Status de campo de conjunto de registros  
 Altera para o valor de uma **campo** objeto da coleção de campos de um uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) são armazenados em cache até que o objeto [atualização](../../../ado/reference/ado-api/update-method.md) método é chamado. Nesse ponto, se a alteração para o valor do campo causou um erro, o OLE DB gera o erro **DB_E_ERRORSOCCURRED** (2147749409). A propriedade de Status de qualquer um dos **campo** objetos na **campos** coleção que causou o erro conterá um valor da [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) que descreve a causa da o problema.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade status (campo) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Exemplo da propriedade Status (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
