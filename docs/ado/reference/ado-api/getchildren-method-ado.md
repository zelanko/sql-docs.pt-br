---
description: Método GetChildren (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 906c20d19143f4f1e8fe0b6c1e91585893acfa5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443578"
---
# <a name="getchildren-method-ado"></a>Método GetChildren (ADO)
Retorna um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) cujas linhas representam os filhos de um [registro](../../../ado/reference/ado-api/record-object-ado.md)de coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto **Recordset** para o qual cada linha representa um filho do objeto de **registro** atual. Por exemplo, os filhos de um **registro** que representa um diretório seriam os arquivos e subdiretórios contidos no diretório pai.  
  
## <a name="remarks"></a>Comentários  
 O provedor determina quais colunas existem no conjunto de **registros**retornado. Por exemplo, um provedor de origem de documento sempre retorna um **conjunto de registros**de recurso.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::
