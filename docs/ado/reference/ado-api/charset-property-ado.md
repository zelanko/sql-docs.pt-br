---
title: Propriedade de conjunto de caracteres (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Stream::Charset
helpviewer_keywords: Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ded981a9ed4905aa607d8b19fe010682b61b5780
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="charset-property-ado"></a>Propriedade de conjunto de caracteres (ADO)
Indica o caractere definido no qual o conteúdo de um texto [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) deve ser convertido para o armazenamento em buffer interno do **fluxo** objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que especifica o caractere definido no qual o conteúdo do **fluxo** será convertido. O valor padrão é **Unicode**. Valores permitidos são típicas cadeias de caracteres passadas através da interface como nomes de conjunto de caracteres da Internet (por exemplo, "iso 8859-1", "Windows-1252" e assim por diante). Para obter uma lista dos nomes de conjunto de caracteres que são conhecidos por um sistema, consulte as subchaves da HKEY_CLASSES_ROOT\MIME\Database\Charset no registro do Windows.  
  
## <a name="remarks"></a>Comentários  
 Um texto **fluxo** do objeto, os dados de texto são armazenados no conjunto de caracteres especificado pelo **Charset** propriedade. O padrão é Unicode. O **Charset** propriedade é usada para converter os dados sendo transferidos para o **fluxo** ou próximo do **fluxo**. Por exemplo, se o **fluxo** contém dados de ISO 8859-1 e que os dados são copiados para um BSTR, o **fluxo** objeto converterá os dados em Unicode. O inverso também é verdadeiro.  
  
 Para que a abertura **fluxo**, atual [posição](../../../ado/reference/ado-api/position-property-ado.md) deve estar no início do **fluxo** (0) para poder definir **Charset**.  
  
 **Conjunto de caracteres** é usado somente com texto **fluxo** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**). Essa propriedade será ignorada se **tipo** é **adTypeBinary**.  
  
 Para obter um exemplo de código, consulte [etapa 4: preencher a caixa de texto detalhes](../../../ado/guide/data/step-4-populate-the-details-text-box.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
