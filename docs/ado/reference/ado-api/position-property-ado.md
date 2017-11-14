---
title: Posicione a propriedade (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76a3d94b97fa32e372cd6cc67367450d2f62530b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="position-property-ado"></a>Propriedade Position (ADO)
Indica a posição atual dentro de um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **longo** valor que especifica o deslocamento, em número de bytes, da posição atual do início do fluxo. O padrão é 0, que representa o primeiro byte no fluxo.  
  
## <a name="remarks"></a>Comentários  
 A posição atual pode ser movida para um ponto após o final do fluxo. Se você especificar a posição atual além do fim do fluxo de [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) do **fluxo** objeto aumentará adequadamente. Qualquer novo bytes adicionados dessa forma, será nulos.  
  
> [!NOTE]
>  **Posição** sempre mede bytes. Para fluxos de texto usando conjuntos de caracteres multibyte, multiplique a posição pelo tamanho de caractere para determinar o número de caracteres. Por exemplo, para um conjunto de caracteres de dois bytes, o primeiro caractere está na posição 0, o segundo caractere na posição 2, o terceiro caractere na posição 4 e assim por diante.  
  
> [!NOTE]
>  Valores negativos não podem ser usados para alterar a posição atual em um **fluxo**. Somente números positivos podem ser usados para **posição**.  
  
> [!NOTE]
>  Para somente leitura **fluxo** objetos, o ADO não retornará um erro se **posição** é definido como um valor maior do que o **tamanho** do **fluxo**. Isso não altera o tamanho do **fluxo**, ou alterar o **fluxo** conteúdo de qualquer maneira. No entanto, isso deve ser evitado porque resulta em um sentido **posição**valor.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Charset (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)

