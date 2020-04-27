---
title: Propriedade Size (fluxo ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e52d05cdbc0fe0ca397c3a7b417fec72703b8e1d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916937"
---
# <a name="size-property-ado-stream"></a>Propriedade Size (Fluxo do ADO)
Indica o tamanho do fluxo em número de bytes.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor **longo** que especifica o tamanho do fluxo em número de bytes. O valor padrão é o tamanho do fluxo, ou-1 se o tamanho do fluxo não for conhecido.  
  
## <a name="remarks"></a>Comentários  
 O **tamanho** pode ser usado somente com objetos de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) aberto.  
  
> [!NOTE]
>  Qualquer número de bits pode ser armazenado em um objeto de **fluxo** , limitado apenas por recursos do sistema. Se o **fluxo** contiver mais bits do que pode ser representado por um valor **longo** , o **tamanho** será truncado e, portanto, não representará com precisão o comprimento do **fluxo**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Size (Parâmetro ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
