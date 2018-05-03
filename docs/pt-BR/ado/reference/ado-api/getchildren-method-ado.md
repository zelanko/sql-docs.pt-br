---
title: Método GetChildren (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 170f17c66ea05a3df7dc6135918d164bd66f993e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getchildren-method-ado"></a>Método GetChildren (ADO)
Retorna um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) cujas linhas representam os filhos de uma coleção [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **registros** objeto para o qual cada linha representa um filho do atual **registro** objeto. Por exemplo, os filhos de um **registro** que representa um diretório será a arquivos e subdiretórios contidos no diretório pai.  
  
## <a name="remarks"></a>Remarks  
 O provedor determina quais colunas existem na retornado **registros**. Por exemplo, um provedor de origem do documento sempre retorna um recurso **registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
