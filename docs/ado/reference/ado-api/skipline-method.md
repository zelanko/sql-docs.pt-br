---
title: Método SkipLine | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 39f17727973a5ada4f28c8ff4b50d13bb5e991e7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711225"
---
# <a name="skipline-method"></a>Método SkipLine
Ignora uma linha inteira durante a leitura de um texto [Stream](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Comentários  
 Todos os caracteres até e incluindo o separador de linha próximo são ignorados. Por padrão, o [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) é **adCRLF**. Se você tentar ignorar [EOS](../../../ado/reference/ado-api/eos-property.md), a posição atual permanecerá nessa **EOS**.  
  
 O **SkipLine** método é usado com fluxos de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) está **adTypeText**).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
