---
title: Propriedade LineSeparator (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Stream::LineSeparator
helpviewer_keywords: LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 183f0847a6a70ff5191b7fb0755c928448ffa3ba
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="lineseparator-property-ado"></a>Propriedade LineSeparator (ADO)
Indica o caractere binário a ser usado como separador de linha no texto [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) valor que indica o caractere de separador de linha usado no **fluxo**. O valor padrão é **adCRLF**.  
  
## <a name="remarks"></a>Remarks  
 **LineSeparator** é usada para interpretar linhas ao ler o conteúdo de um texto **fluxo**. Linhas podem ser ignoradas com o [SkipLine](../../../ado/reference/ado-api/skipline-method.md) método.  
  
 **LineSeparator** é usado somente com texto **fluxo** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**). Essa propriedade será ignorada se **tipo** é **adTypeBinary**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
