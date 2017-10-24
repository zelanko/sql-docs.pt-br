---
title: "Método GetChildren (ADO) | Microsoft Docs"
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
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 84f146c110b50cc3c73329dd72feb26f1ebf3858
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getchildren-method-ado"></a>Método GetChildren (ADO)
Retorna um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) cujas linhas representam os filhos de uma coleção [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **registros** objeto para o qual cada linha representa um filho do atual **registro** objeto. Por exemplo, os filhos de um **registro** que representa um diretório será a arquivos e subdiretórios contidos no diretório pai.  
  
## <a name="remarks"></a>Comentários  
 O provedor determina quais colunas existem na retornado **registros**. Por exemplo, um provedor de origem do documento sempre retorna um recurso **registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|

