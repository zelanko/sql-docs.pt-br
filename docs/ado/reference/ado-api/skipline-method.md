---
title: Método de ignorar | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8439f7d8fabc5675e43fca5bba006b22574b992
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931043"
---
# <a name="skipline-method"></a>Método SkipLine
Ignora uma linha inteira ao ler um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md)de texto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Comentários  
 Todos os caracteres até e incluindo o próximo separador de linha são ignorados. Por padrão, o [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) é **adCRLF**. Se você tentar ignorar o [EOS](../../../ado/reference/ado-api/eos-property.md)anterior, a posição atual permanecerá no **EOS**.  
  
 O método de **ignorar** é usado com fluxos de texto (o[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
