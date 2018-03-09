---
title: "Excluir método (coleção de parâmetros de ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5b7aff01cf3bb0dd34c53986a586aeae7b499a6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="delete-method-ado-parameters-collection"></a>Excluir método (coleção de parâmetros do ADO)
Exclui um objeto a partir de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Index*  
 Um **cadeia de caracteres** valor que contém o nome do objeto que deseja excluir, ou a posição do objeto ordinal (índice) na coleção.  
  
## <a name="remarks"></a>Remarks  
 Usando o **excluir** método em uma coleção permite que você remova um dos objetos na coleção. Este método está disponível apenas no **parâmetros** coleção de um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Você deve usar o [parâmetro](../../../ado/reference/ado-api/parameter-object.md) do objeto [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade ou o índice de coleção ao chamar o **excluir** método — uma variável de objeto não é um argumento válido.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Delete (coleção de campos do ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
