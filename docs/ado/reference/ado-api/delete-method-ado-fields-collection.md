---
description: Método Delete (Coleção de campos ADO)
title: Método Delete (coleção de campos ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
author: rothja
ms.author: jroth
ms.openlocfilehash: fb60cea6ef2e741103e94f38955bb2afc688e228
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444168"
---
# <a name="delete-method-ado-fields-collection"></a>Método Delete (Coleção de campos ADO)
Exclui um objeto da coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Campo*  
 Uma **variante** que designa o objeto de [campo](../../../ado/reference/ado-api/field-object.md) a ser excluído. Esse parâmetro pode ser o nome do objeto de **campo** ou a posição ordinal do próprio objeto **Field** .  
  
## <a name="remarks"></a>Comentários  
 Chamar o método **Fields. Delete** em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) aberto causa um erro em tempo de execução.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Delete (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método Delete (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
