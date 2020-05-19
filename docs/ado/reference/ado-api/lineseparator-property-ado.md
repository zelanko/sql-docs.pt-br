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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9248dcabb4c52ceceb6e4876b034480415e77963
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754814"
---
# <a name="lineseparator-property-ado"></a>Propriedade LineSeparator (ADO)
Indica o caractere binário a ser usado como separador de linha em objetos de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) de texto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) que indica o caractere separador de linha usado no **fluxo**. O valor padrão é **adCRLF**.  
  
## <a name="remarks"></a>Comentários  
 **LineSeparator** é usado para interpretar linhas ao ler o conteúdo de um **fluxo**de texto. As linhas podem ser ignoradas com o método de [ignorar](../../../ado/reference/ado-api/skipline-method.md) .  
  
 **LineSeparator** é usado somente com objetos de **fluxo** de texto (o[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**). Essa propriedade será ignorada se o **tipo** for **adTypeBinary**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
