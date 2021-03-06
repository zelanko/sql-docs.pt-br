---
description: Método Delete (Coleção de parâmetros ADO)
title: Método Delete (coleção de parâmetros ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3860a824690d9dca469a22135d35e040cc000dca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974117"
---
# <a name="delete-method-ado-parameters-collection"></a>Método Delete (Coleção de parâmetros ADO)
Exclui um objeto da coleção de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Index*  
 Um valor de **cadeia de caracteres** que contém o nome do objeto que você deseja excluir ou a posição ordinal do objeto (índice) na coleção.  
  
## <a name="remarks"></a>Comentários  
 O uso do método **delete** em uma coleção permite remover um dos objetos da coleção. Esse método está disponível apenas na coleção **Parameters** de um objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) . Você deve usar a propriedade [Name](../../../ado/reference/ado-api/name-property-ado.md) do objeto de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) ou seu índice de coleção ao chamar o método **delete** – uma variável de objeto não é um argumento válido.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
