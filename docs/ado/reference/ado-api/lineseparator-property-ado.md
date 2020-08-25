---
description: Propriedade LineSeparator (ADO)
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
ms.openlocfilehash: fe0976fda4a390f93f7d634fac9e1cbc52104b29
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774625"
---
# <a name="lineseparator-property-ado"></a>Propriedade LineSeparator (ADO)
Indica o caractere binário a ser usado como separador de linha em objetos de [fluxo](./stream-object-ado.md) de texto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor [LineSeparatorsEnum](./lineseparatorsenum.md) que indica o caractere separador de linha usado no **fluxo**. O valor padrão é **adCRLF**.  
  
## <a name="remarks"></a>Comentários  
 **LineSeparator** é usado para interpretar linhas ao ler o conteúdo de um **fluxo**de texto. As linhas podem ser ignoradas com o método de [ignorar](./skipline-method.md) .  
  
 **LineSeparator** é usado somente com objetos de **fluxo** de texto (o[tipo](./type-property-ado-stream.md) é **adTypeText**). Essa propriedade será ignorada se o **tipo** for **adTypeBinary**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Stream (ADO)](./stream-object-ado.md)