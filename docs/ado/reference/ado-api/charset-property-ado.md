---
title: Propriedade charset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20fff124f33bfeccaec665c74687753e2c0af20b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239748"
---
# <a name="charset-property-ado"></a>Propriedade Charset (ADO)
Indica o caractere definido na qual o conteúdo de um texto [Stream](../../../ado/reference/ado-api/stream-object-ado.md) deve ser convertido para o armazenamento em buffer interno do **Stream** objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que especifica o caractere definido na qual o conteúdo do **Stream** será convertido. O valor padrão é **Unicode**. Os valores permitidos são típicas cadeias de caracteres passadas pela interface como nomes de conjunto de caracteres de Internet (por exemplo, "iso-8859-1", "Windows-1252" e assim por diante). Para obter uma lista dos nomes de conjunto de caracteres que são conhecidos por um sistema, consulte as subchaves da HKEY_CLASSES_ROOT\MIME\Database\Charset no registro do Windows.  
  
## <a name="remarks"></a>Comentários  
 Em um texto **Stream** do objeto, dados de texto são armazenados no conjunto de caracteres especificado pela **Charset** propriedade. O padrão é Unicode. O **Charset** propriedade é usada para a conversão de dados que entram as **Stream** ou próximos da **Stream**. Por exemplo, se o **Stream** contém dados de ISO-8859-1 e que os dados são copiados para um BSTR, o **Stream** objeto converterá os dados em Unicode. O inverso também é verdadeiro.  
  
 Para que a abertura **Stream**, atual [posição](../../../ado/reference/ado-api/position-property-ado.md) deve ser no início do **Stream** (0) para poder definir **Charset**.  
  
 **Charset** é usado apenas com texto **Stream** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**). Essa propriedade será ignorada se **tipo** é **adTypeBinary**.  
  
 Para obter um exemplo de código, consulte [etapa 4: Preencha a caixa de texto de detalhes](../../../ado/guide/data/step-4-populate-the-details-text-box.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
