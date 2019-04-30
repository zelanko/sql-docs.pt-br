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
manager: craigg
ms.openlocfilehash: 097286f14de4dead4490c322615a6405c157f118
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140255"
---
# <a name="delete-method-ado-fields-collection"></a>Método Delete (Coleção de campos ADO)
Exclui um objeto a partir de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Campo*  
 Um **Variant** que designa a [campo](../../../ado/reference/ado-api/field-object.md) objeto a ser excluído. Esse parâmetro pode ser o nome da **campo** objeto ou a posição ordinal do **campo** objeto propriamente dito.  
  
## <a name="remarks"></a>Comentários  
 Chamar o **Fields.Delete** método em um aberto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) causa um erro de tempo de execução.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Excluir método (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
