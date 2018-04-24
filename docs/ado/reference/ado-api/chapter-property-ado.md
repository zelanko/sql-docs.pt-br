---
title: Propriedade de capítulo (ADO) | Microsoft Docs
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
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7cfa863254391760a45f8857f002ac92f25dd07
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="chapter-property-ado"></a>Propriedade de capítulo (ADO)
Obtém ou define um banco de dados OLE **capítulo** objeto de/em uma [ADORecordsetConstruction Interface](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md) objeto. Quando você usa **put_Chapter** para definir o **capítulo** do objeto, um subconjunto de linhas é transformado em ADO [objeto Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Isso define o capítulo atual o **linhas**objeto. Esta propriedade é leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *plChapter*  
 Ponteiro para o identificador de um capítulo.  
  
 *LChapter*  
 Identificador de um capítulo.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
