---
title: Método Delete (coleção de campos de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 296364d3fafc4a67767699d55631209658657de1
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277545"
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
  
## <a name="remarks"></a>Remarks  
 Chamando o **Fields.Delete** método em um aberto [registros](../../../ado/reference/ado-api/recordset-object-ado.md) causa um erro de tempo de execução.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Excluir método (coleção de parâmetros do ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
