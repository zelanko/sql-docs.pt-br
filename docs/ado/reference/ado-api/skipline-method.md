---
description: Método SkipLine
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
ms.openlocfilehash: c0897d90ffeccabbce57525f268214577a523d92
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777465"
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