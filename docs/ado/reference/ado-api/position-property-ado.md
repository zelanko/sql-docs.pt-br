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
manager: jroth
ms.openlocfilehash: 7b777179ad83250d9707f7717b5833bbbff4fec7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703407"
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
