---
description: Propriedade Position (ADO)
title: Propriedade Position (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 55ae275db06b8b0c73598977e78954bac0fd22be
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990057"
---
# <a name="position-property-ado"></a>Propriedade Position (ADO)
Indica a posição atual em um objeto de [fluxo](./stream-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que especifica o deslocamento, em número de bytes, da posição atual do início do fluxo. O padrão é 0, que representa o primeiro byte no fluxo.  
  
## <a name="remarks"></a>Comentários  
 A posição atual pode ser movida para um ponto após o fim do fluxo. Se você especificar a posição atual além do fim do fluxo, o [tamanho](./size-property-ado-stream.md) do objeto de **fluxo** será aumentado de acordo. Todos os novos bytes adicionados dessa maneira serão nulos.  
  
> [!NOTE]
>  **Position** sempre mede bytes. Para fluxos de texto usando conjuntos de caracteres multibyte, multiplique a posição pelo tamanho do caractere para determinar o número do caractere. Por exemplo, para um conjunto de caracteres de dois bytes, o primeiro caractere está na posição 0, o segundo caractere na posição 2, o terceiro caractere na posição 4 e assim por diante.  
  
> [!NOTE]
>  Valores negativos não podem ser usados para alterar a posição atual em um **fluxo**. Somente números positivos podem ser usados para a **posição**.  
  
> [!NOTE]
>  Para objetos de **fluxo** somente leitura, o ADO não retornará um erro se a **posição** for definida como um valor maior que o **tamanho** do **fluxo**. Isso não altera o tamanho do **fluxo**nem altera o conteúdo do **fluxo** de forma alguma. No entanto, isso deve ser evitado porque resulta em um valor de **posição**sem sentido.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Charset (ADO)](./charset-property-ado.md)