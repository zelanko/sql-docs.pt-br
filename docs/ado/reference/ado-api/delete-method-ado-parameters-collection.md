---
title: Excluir método (coleção de parâmetros ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8eb7d5d58e0f6afe31304b6fce13da2d8c48e54e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696915"
---
# <a name="delete-method-ado-parameters-collection"></a>Método Delete (Coleção de parâmetros ADO)
Exclui um objeto a partir de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Index*  
 Um **cadeia de caracteres** valor que contém o nome do objeto que deseja excluir, ou a posição do objeto ordinal (índice) na coleção.  
  
## <a name="remarks"></a>Comentários  
 Usando o **excluir** método em uma coleção permite que você remova um dos objetos na coleção. Esse método está disponível apenas na **parâmetros** coleção de uma [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Você deve usar o [parâmetro](../../../ado/reference/ado-api/parameter-object.md) do objeto [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade ou o índice de coleção ao chamar o **excluir** método — uma variável de objeto não é um argumento válido.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
