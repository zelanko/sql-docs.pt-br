---
title: Propriedade Chapter (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 37d1fe31524d245da2a6bac9b90ab2e680fab450
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696147"
---
# <a name="chapter-property-ado"></a>Propriedade Chapter (ADO)
Obtém ou define um banco de dados OLE **capítulo** objeto de/em uma [ADORecordsetConstruction Interface](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md) objeto. Quando você usa **put_Chapter** para definir o **capítulo** do objeto, um subconjunto de linhas é transformado em ADO [objeto Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Isso define o capítulo atual de **conjunto de linhas**objeto. Esta propriedade é leitura/gravação.  
  
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
