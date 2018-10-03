---
title: Método CopyTo (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad973b69d9f85b731e417e502225036ae714ae63
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658637"
---
# <a name="copyto-method-ado"></a>Método CopyTo (ADO)
Copia o número especificado de caracteres ou bytes (dependendo da [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md)) na [Stream](../../../ado/reference/ado-api/stream-object-ado.md) para outra **Stream** objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DestStream*  
 Um valor de variável de objeto que contém uma referência a um aberto **Stream** objeto. O atual **Stream** é copiado para o destino **Stream** especificado por *DestStream*. O destino **Stream** já deve estar aberta. Se não, ocorrerá um erro de tempo de execução.  
  
> [!NOTE]
>  O *DestStream* parâmetro não pode ser um proxy do **Stream** porque isso requer acesso a uma interface privada no **Stream** objeto não pode ser remoto para o cliente.  
  
 *NumChars*  
 Opcional. Uma **inteiro** valor que especifica o número de bytes ou caracteres a serem copiados da posição atual na fonte **Stream** para o destino **Stream**. O valor padrão é -1, que especifica que todos os caracteres ou bytes são copiados da posição atual para [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Comentários  
 Esse método copia o número especificado de caracteres ou bytes, começando da posição atual especificada pela [posição](../../../ado/reference/ado-api/position-property-ado.md) propriedade. Se o número especificado é maior que o número de bytes até disponíveis **EOS**, em seguida, apenas caracteres ou bytes a partir da posição atual para **EOS** são copiados. Se o valor de *NumChars* é -1 ou omitido, todos os caracteres ou bytes, começando da posição atual são copiados.  
  
 Se houver caracteres ou bytes no fluxo de destino, todo o conteúdo além do momento em que a cópia termina permanece e não é truncado. **Posição** torna-se o byte imediatamente após o último byte copiado. Se você deseja truncar esses bytes, chame [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 **CopyTo** deve ser usado para copiar dados para um destino **Stream** do mesmo tipo como a fonte **Stream** (seus **tipo** as configurações de propriedade são os dois **adTypeText** ou ambos **adTypeBinary**). Para texto **Stream** objetos, você pode alterar o [Charset](../../../ado/reference/ado-api/charset-property-ado.md) configuração da propriedade de destino **Stream** traduzir de um conjunto de caracteres para outra. Além disso, o texto **Stream** objetos podem ser copiados com êxito para o binário **Stream** objetos, mas binário **Stream** objetos não podem ser copiados em texto **Stream**  objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
