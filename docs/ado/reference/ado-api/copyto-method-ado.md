---
title: Método CopyTo (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32e889ea84c02a544ccad53cd9c274c360994bfe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="copyto-method-ado"></a>Método CopyTo (ADO)
Copia o número especificado de caracteres ou bytes (dependendo da [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md)) no [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) para outro **fluxo** objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DestStream*  
 Um valor de variável de objeto que contém uma referência a um aberto **fluxo** objeto. Atual **fluxo** é copiado para o destino **fluxo** especificado por *DestStream*. O destino **fluxo** já deve estar aberta. Se não, ocorrerá um erro de tempo de execução.  
  
> [!NOTE]
>  O *DestStream* parâmetro não pode ser um proxy de **fluxo** porque isso requer acesso a uma interface privada no **fluxo** objeto não pode ser remoto para o cliente.  
  
 *NumChars*  
 Opcional. Um **inteiro** valor que especifica o número de bytes ou caracteres a serem copiados a partir da posição atual na fonte de **fluxo** para o destino **fluxo**. O valor padrão é -1, que especifica que todos os caracteres ou bytes são copiados da posição atual para [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Remarks  
 Esse método copia o número especificado de caracteres ou bytes, começando a partir da posição atual especificada pelo [posição](../../../ado/reference/ado-api/position-property-ado.md) propriedade. Se o número especificado é maior que o número de bytes até disponíveis **EOS**, em seguida, apenas caracteres ou bytes a partir da posição atual para **EOS** são copiados. Se o valor de *NumChars* será – 1 ou omitido, todos os caracteres ou bytes a partir da posição atual são copiados.  
  
 Se houver caracteres ou bytes no fluxo de destino, todo o conteúdo além do ponto em que a cópia termina permanecem e não é truncado. **Posição** torna-se o byte imediatamente após o último byte copiado. Se você deseja truncar esses bytes, chame [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 **CopyTo** deve ser usado para copiar dados para um destino **fluxo** o mesmo tipo da fonte de **fluxo** (seus **tipo** as configurações de propriedade são ambos **adTypeText** ou ambos **adTypeBinary**). Para texto **fluxo** objetos, você pode alterar o [Charset](../../../ado/reference/ado-api/charset-property-ado.md) configuração da propriedade de destino **fluxo** para converter de um conjunto para outro. Além disso, o texto **fluxo** objetos podem ser copiados com êxito em binário **fluxo** objetos, mas binário **fluxo** objetos não podem ser copiados em texto **fluxo**  objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
