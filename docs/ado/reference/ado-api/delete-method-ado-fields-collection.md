---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9db49905b6548e5cb21cca976683c8b387017d32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919129"
---
# <a name="delete-method-ado-fields-collection"></a>Método Delete (Coleção de campos ADO)
Exclui um objeto da coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>parâmetros  
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
