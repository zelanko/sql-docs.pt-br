---
description: Propriedade Chapter (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 04469dc7cc888a167135ad18a77469200614e925
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776295"
---
# <a name="chapter-property-ado"></a>Propriedade Chapter (ADO)
Obtém ou define um objeto de **capítulo** de OLE DB de/em um objeto de [interface ADORecordsetConstruction](./adorecordsetconstruction-interface.md) . Quando você usa **put_Chapter** para definir o objeto do **capítulo** , um subconjunto de linhas é transformado em um objeto de [objeto Recordset](./recordset-object-ado.md) do ADO. Isso define o capítulo atual do objeto **Rowset**. Esta propriedade é de leitura/gravação.  
  
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
 Esse método de propriedade retorna os valores de HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Interface ADORecordsetConstruction](./adorecordsetconstruction-interface.md)