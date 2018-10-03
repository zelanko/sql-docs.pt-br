---
title: Propriedade LineSeparator (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b55f82e92ff74ba359074613205bc8086af81b5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639354"
---
# <a name="lineseparator-property-ado"></a>Propriedade LineSeparator (ADO)
Indica o caractere binário a ser usado como o separador de linha no texto [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) valor que indica o caractere de separador de linha usado na **Stream**. O valor padrão é **adCRLF**.  
  
## <a name="remarks"></a>Comentários  
 **LineSeparator** é usada para interpretar linhas ao ler o conteúdo de um texto **Stream**. Linhas podem ser ignoradas com o [SkipLine](../../../ado/reference/ado-api/skipline-method.md) método.  
  
 **LineSeparator** é usado apenas com texto **Stream** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**). Essa propriedade será ignorada se **tipo** é **adTypeBinary**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
