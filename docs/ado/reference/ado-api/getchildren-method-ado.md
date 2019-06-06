---
title: Método GetChildren (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d29618fbacfbd4ba3becd222ef8a063e59e2cc70
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697836"
---
# <a name="getchildren-method-ado"></a>Método GetChildren (ADO)
Retorna um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) cujas linhas representam os filhos de uma coleção [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **conjunto de registros** objeto para o qual cada linha representa um filho do atual **registro** objeto. Por exemplo, os filhos de um **registro** que representa um diretório seria os arquivos e subdiretórios contidos no diretório pai.  
  
## <a name="remarks"></a>Comentários  
 O provedor determina quais colunas existem na retornado **conjunto de registros**. Por exemplo, um provedor de origem do documento sempre retorna um recurso **conjunto de registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
