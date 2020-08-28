---
description: Propriedade Charset (ADO)
title: Propriedade charset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
author: rothja
ms.author: jroth
ms.openlocfilehash: 52daa13826bbe372b141501a0c99ac281d3118dc
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975497"
---
# <a name="charset-property-ado"></a>Propriedade Charset (ADO)
Indica o conjunto de caracteres no qual o conteúdo de um [fluxo](./stream-object-ado.md) de texto deve ser convertido para armazenamento no buffer interno do objeto de **fluxo** .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que especifica o conjunto de caracteres no qual o conteúdo do **fluxo** será traduzido. O valor padrão é **Unicode**. Os valores permitidos são cadeias de caracteres típicas passadas pela interface como nomes de conjunto de caractere da Internet (por exemplo, "ISO-8859-1", "Windows-1252" e assim por diante). Para obter uma lista dos nomes de conjunto de caracteres que são conhecidos por um sistema, consulte as subchaves de HKEY_CLASSES_ROOT \MIME\Database\Charset no registro do Windows.  
  
## <a name="remarks"></a>Comentários  
 Em um objeto de **fluxo** de texto, os dados de texto são armazenados no conjunto de caracteres especificado pela propriedade **charset** . O padrão é Unicode. A propriedade **charset** é usada para converter dados que entram no **fluxo** ou saindo do **fluxo**. Por exemplo, se o **fluxo** contiver dados ISO-8859-1 e esses dados forem copiados para um BSTR, o objeto de **fluxo** converterá os dados em Unicode. O inverso também é verdadeiro.  
  
 Para um **fluxo**aberto, a [posição](./position-property-ado.md) atual deve estar no início do **fluxo** (0) para poder definir **charset**.  
  
 O conjunto de **caracteres** é usado somente com objetos de **fluxo** de texto (o[tipo](./type-property-ado-stream.md) é **adTypeText**). Essa propriedade será ignorada se o **tipo** for **adTypeBinary**.  
  
 Para obter um exemplo de código, consulte [etapa 4: popular a caixa de texto detalhes](../../guide/data/step-4-populate-the-details-text-box.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)