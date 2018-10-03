---
title: Posicione a propriedade (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 333b06ef76ae6407ca8a5605f1917dc0bb609aca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615884"
---
# <a name="position-property-ado"></a>Propriedade Position (ADO)
Indica a posição atual dentro de um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **longo** valor que especifica o deslocamento, em número de bytes, da posição atual do início do fluxo. O padrão é 0, que representa o primeiro byte no fluxo.  
  
## <a name="remarks"></a>Comentários  
 A posição atual pode ser movida para um ponto após o final do fluxo. Se você especificar a posição atual além do fim do fluxo, o [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) da **Stream** objeto aumentará adequadamente. Qualquer novo bytes adicionados dessa maneira, será nulos.  
  
> [!NOTE]
>  **Posição** sempre mede bytes. Para fluxos de texto usando conjuntos de caracteres multibyte, multiplique a posição pelo tamanho do caractere para determinar o número de caracteres. Por exemplo, para um conjunto de caracteres de dois bytes, o primeiro caractere está na posição 0, o segundo caractere na posição 2, o terceiro caractere na posição 4 e assim por diante.  
  
> [!NOTE]
>  Valores negativos não podem ser usados para alterar a posição atual em um **Stream**. Apenas números positivos podem ser usados para **posição**.  
  
> [!NOTE]
>  Para somente leitura **Stream** objetos, o ADO não retornará um erro se **posição** é definido como um valor maior que o **tamanho** do **Stream**. Isso não altera o tamanho do **Stream**, ou alterar as **Stream** conteúdo de qualquer maneira. No entanto, isso deve ser evitado porque ele resulta em um sentido **posição**valor.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Charset (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
