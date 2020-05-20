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
author: rothja
ms.author: jroth
ms.openlocfilehash: f983646fd87be27fe9861f3a37b0e852a05ba06b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759872"
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
