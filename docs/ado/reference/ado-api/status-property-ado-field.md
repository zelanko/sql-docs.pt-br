---
description: Propriedade Status (campo ADO)
title: Propriedade Status (campo ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 11f59e99eab0a742a4d7618f7ac66cb486af2933
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988717"
---
# <a name="status-property-ado-field"></a>Propriedade Status (campo ADO)
Indica o status de um objeto de [campo](./field-object.md) .  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor [FieldStatusEnum](./fieldstatusenum.md) . O valor padrão é **adFieldOK**.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="record-field-status"></a>Status do campo de registro  
 As alterações no valor de um objeto de **campo** na coleção Fields de um objeto de [registro](./record-object-ado.md) são armazenadas em cache até que o método [Update](./update-method.md) do objeto seja chamado. Nesse ponto, se a alteração no valor do campo tiver causado um erro, OLE DB gerará o erro **DB_E_ERRORSOCCURRED** (2147749409). A propriedade status de qualquer um dos objetos **Field** na coleção **Fields** que causou o erro conterá um valor de [FieldStatusEnum](./fieldstatusenum.md) que descreve a causa do problema.  
  
 Para aprimorar o desempenho, adições e exclusões para as coleções de [campos](./fields-collection-ado.md) do objeto de **registro** são armazenadas em cache até que o método de **atualização** seja chamado e, em seguida, as alterações sejam feitas em uma atualização otimista em lote. Se o método **Update** não for chamado, o servidor não será atualizado. Se alguma atualização falhar, um erro do provedor de OLE DB (DB_E_ERRORSOCCURRED) será retornado e a propriedade **status** indicará os valores combinados da operação e do código de status de erro. Por exemplo, **ADFIELDPENDINGINSERT ou adFieldPermissionDenied**. A propriedade **status** de cada **campo** pode ser usada para determinar por que o **campo** não foi adicionado, modificado ou excluído.  
  
 Muitos tipos de problemas encontrados ao adicionar, modificar ou excluir um **campo** são relatados por meio da propriedade **status** . Por exemplo, se o usuário excluir um **campo**, ele será marcado para exclusão na coleção **campos** . Se a **atualização** subsequente retornar um erro porque o usuário tentou excluir um **campo** para o qual ele não tem permissão, o **campo** terá o **status** de **adFieldPermissionDenied ou adFieldPendingDelete**. Chamar o método [CancelUpdate](./cancelupdate-method-ado.md) restaura os valores originais e define o **status** como **adFieldOK**.  
  
 Da mesma forma, o método **Update** pode retornar um erro porque um novo **campo** foi adicionado e recebeu um valor inadequado. Nesse caso, o novo **campo** estará na coleção **Fields** e terá um status de **AdFieldPendingInsert** e, talvez, **adFieldCantCreate** (dependendo do seu provedor). Você pode fornecer um valor apropriado para o novo **campo** e chamar **Atualizar** novamente.  
  
## <a name="recordset-field-status"></a>Status do campo do conjunto de registros  
 As alterações no valor de um objeto **Field** na coleção Fields de um [conjunto de registros](./recordset-object-ado.md) são armazenadas em cache até que o método [Update](./update-method.md) do objeto seja chamado. Nesse ponto, se a alteração no valor do campo tiver causado um erro, OLE DB gerará o erro **DB_E_ERRORSOCCURRED** (2147749409). A propriedade status de qualquer um dos objetos **Field** na coleção **Fields** que causou o erro conterá um valor de [FieldStatusEnum](./fieldstatusenum.md) que descreve a causa do problema.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](./field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Status (campo) (VB)](./status-property-example-field-vb.md)   
 [Exemplo da propriedade Status (VC++)](./status-property-example-vc.md)