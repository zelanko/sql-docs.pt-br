---
title: Método GetChildren (ADO) | Microsoft Docs
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
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a920d0e7b45394f5714cd8f9df83751a322b9401
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278845"
---
# <a name="getchildren-method-ado"></a>Método GetChildren (ADO)
Retorna um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) cujas linhas representam os filhos de uma coleção [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **registros** objeto para o qual cada linha representa um filho do atual **registro** objeto. Por exemplo, os filhos de um **registro** que representa um diretório será a arquivos e subdiretórios contidos no diretório pai.  
  
## <a name="remarks"></a>Remarks  
 O provedor determina quais colunas existem na retornado **registros**. Por exemplo, um provedor de origem do documento sempre retorna um recurso **registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
