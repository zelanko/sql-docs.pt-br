---
description: Método SkipLine
title: Método de ignorar | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 840c0111aca8b202fd081d3f0250d17fd43e5bbb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989047"
---
# <a name="skipline-method"></a>Método SkipLine
Ignora uma linha inteira ao ler um [fluxo](./stream-object-ado.md)de texto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Comentários  
 Todos os caracteres até e incluindo o próximo separador de linha são ignorados. Por padrão, o [LineSeparator](./lineseparator-property-ado.md) é **adCRLF**. Se você tentar ignorar o [EOS](./eos-property.md)anterior, a posição atual permanecerá no **EOS**.  
  
 O método de **ignorar** é usado com fluxos de texto (o[tipo](./type-property-ado-stream.md) é **adTypeText**).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)