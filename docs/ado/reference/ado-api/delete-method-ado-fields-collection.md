---
title: "Método Delete (coleção de campos de ADO) | Microsoft Docs"
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
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: de4e5f85bad4849f4ace2ee4e32fbe6606cb667d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="delete-method-ado-fields-collection"></a>Método Delete (coleção de campos do ADO)
Exclui um objeto a partir de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Campo*  
 Um **Variant** que designa o [campo](../../../ado/reference/ado-api/field-object.md) objeto a ser excluído. Esse parâmetro pode ser o nome do **campo** objeto ou a posição ordinal do **campo** objeto propriamente dito.  
  
## <a name="remarks"></a>Comentários  
 Chamando o **Fields.Delete** método em um aberto [registros](../../../ado/reference/ado-api/recordset-object-ado.md) causa um erro de tempo de execução.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Excluir método (coleção de parâmetros do ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

